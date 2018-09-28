/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pkg2;


import java.util.concurrent.Semaphore;
public class Main {

    

     static int rc=0;
    static Semaphore r = new Semaphore(1);
   static Semaphore wrt = new Semaphore(1);
    

    static class Reader implements Runnable {
       
       public void run() {
            try {
               
                r.acquire();
                rc=rc+1;
                if (rc == 1) {
                    wrt.acquire();
                }
                r.release();

               
                System.out.println("Thread "+Thread.currentThread().getName() + " is READING");
                Thread.sleep(1500);
                System.out.println("Thread "+Thread.currentThread().getName() + " has FINISHED READING");

               
                r.acquire();
                rc=rc-1;
                if(rc == 0) {
                    wrt.release();
                }
                r.release();
            } 
            catch (InterruptedException e) 
            {
                System.out.println(e.getMessage());
            }
        }
    }

    static class Writer implements Runnable {
        
        public void run() {
            try {
                wrt.acquire();
                System.out.println("Thread "+Thread.currentThread().getName() + " is WRITING");
                Thread.sleep(1000);
                System.out.println("Thread "+Thread.currentThread().getName() + " has finished WRITING");
                wrt.release();
            } 
            catch (InterruptedException e) {
                System.out.println(e.getMessage());
            }
        }
    }

    public static void main(String[] args) throws Exception {
        Reader r = new Reader();
        Writer w = new Writer();
        Thread t1 = new Thread(r);
        t1.setName("t1");
        Thread t2 = new Thread(r);
        t2.setName("t2");
        Thread t3 = new Thread(w);
        t3.setName("t3");
       Thread t4 = new Thread(r);
       t4.setName("t4");
        t1.start();
        t3.start();
        t2.start();
        t4.start();
    }
}

    
    






