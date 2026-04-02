```java
public class Main {

    public static void main(String[] args) {

       List<Integer> numList = new ArrayList<>();
       numList.add(3);
       System.out.println(numList.size());

       Map<String,Integer> map = new HashMap<>();
       map.put("banana",1);
       System.out.println(map.get("banana"));

       Set<Integer> set = new HashSet<>();
       set.add(2);
       set.add(2);
       set.add(4);
       set.add(4);
       System.out.println(set);

       Queue<Integer> queue = new LinkedList<>();
       System.out.println("Before offer:" + queue);
       queue.offer(200);
       System.out.println("After offer:" + queue);
       Integer polled = queue.poll();
       System.out.println("Polled = " + polled);
       System.out.println("After poll:" + queue);

       ArrayDeque<Integer> stack = new ArrayDeque<>();
       stack.push(1);
       stack.push(2);
       stack.push(3);
       stack.pop();
       stack.pop();
       Integer remaining = stack.peek();
       System.out.println("Remaining = " + remaining);

       PriorityQueue<Integer> minPq = new PriorityQueue<>();
       minPq.add(4);
       minPq.add(9);
       minPq.add(2);
       minPq.add(6);
       minPq.add(12);
       Integer smallest = minPq.poll();
       System.out.println("Smallest = " + smallest);

    }
}

```
