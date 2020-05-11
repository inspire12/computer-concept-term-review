# Java NIO 

Java New IO 
Non-blocking = Stream : Channel

## Stream Vs Channel 
공통점: 데이터가 흘러다니는 통로 

* Stream은 단방향 

InputStream 과 OutputStream으로 구분 
Stream을 통해 흘러다니는 데이터는 byte[] 
작업이 끝나야 return 되는 blocking 

* Channel은 양방향
  
Buffer를 통해서만 데이터를 읽고 쓸 수 있다. 
ByteChannel FileChannel 을 만들어서 읽을 수도 있고, 쓸 수도 있다. 

채널은 Non-blocking <b>방식도 가능</b>

Files.new ~~() 는 모두 blocking 이다. 

java.nio.Files는 NIO 중 File I/O를 담당

. java 7 부터 도입되어 NIO2라고 불리는 NIO에는 AsynchronousFileChannel이 Non-blocking 모드로 동작한다. 
 



## Reference
- [Java NIO는 생각만큼 non-blocking 하지 않다](https://homoefficio.github.io/2016/08/06/Java-NIO%EB%8A%94-%EC%83%9D%EA%B0%81%EB%A7%8C%ED%81%BC-non-blocking-%ED%95%98%EC%A7%80-%EC%95%8A%EB%8B%A4/)
- [Java API > NIO](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/ReadableByteChannel.html)