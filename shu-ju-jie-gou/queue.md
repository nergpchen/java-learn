Queue:

 先进先出是队列.  


public class Queues {

  


private Node first ,last;



 private class Node {

private String item;

private Node next;

 }



publicvoid enqueue\(String item\) {

 Node oldLast = last;

last = new Node\(\);

 last.item =item;

 last.next =null;



if\(isEmpty\(\)\) {

first = last;

first.next=null;

 }else {

oldLast.next = last;

 }

 }



publicboolean isEmpty\(\) {

returnfirst == null;

 }



public String dequeue\(\) {

 String item = first.item;

first = first.next;

if \(isEmpty\(\)\) last = null;

returnitem;

 }

}

