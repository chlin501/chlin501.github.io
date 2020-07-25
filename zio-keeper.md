# Troubleshooting

    * Caused by: java.net.SocketException: Network is unreachable

        ```
        - transport
        [info]   - udp
        [info]     - can send and receive messages
        [info]       Fiber failed.
        [info]       A checked error was not handled.
        [info]       zio.keeper.TransportError$ExceptionWrapper: Exception in transport
        [info]          at zio.keeper.TransportError$ExceptionWrapper$.apply(errors.scala:60)
        ... 
        [info]       Caused by: java.net.SocketException: Network is unreachable
        [info]          at java.base/sun.nio.ch.Net.connect0(Native Method)
        [info]          at java.base/sun.nio.ch.Net.connect(Net.java:476)
        [info]          at java.base/sun.nio.ch.DatagramChannelImpl.connect(DatagramChannelImpl.java:848)
        [info]          at zio.nio.channels.DatagramChannel.$anonfun$connect$1(DatagramChannel.scala:23)
        [info]          at zio.internal.FiberContext.evaluateNow(FiberContext.scala:360)
        [info]          ... 4 more
        ```

        * Solution: `export _JAVA_OPTIONS="-Djava.net.preferIPv4Stack=true"`

# References

  [1]. [How to force Java to use IPv4 instead IPv6?](https://superuser.com/questions/453298/how-to-force-java-to-use-ipv4-instead-ipv6/453329#453329)
