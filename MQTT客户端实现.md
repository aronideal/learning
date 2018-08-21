
Java实现
========

```xml
<dependency>
    <groupId>org.fusesource.mqtt-client</groupId>
    <artifactId>mqtt-client</artifactId>
    <version>1.12</version>
</dependency>
```

客户端
------

```java
        MQTT mqtt = new MQTT();
        mqtt.setHost("ip", 1883);
        final CallbackConnection connection = mqtt.callbackConnection();
        connection.listener(new Listener() {
            @Override
            public void onConnected() {
                System.out.println("connection: onConnected");
            }

            @Override
            public void onPublish(UTF8Buffer topic, Buffer body, Runnable ack) {
                System.out.println("connection: onPublish");

                ack.run();
            }

            @Override
            public void onDisconnected() {
                System.out.println("connection: onDisconnected");
            }

            @Override
            public void onFailure(Throwable value) {
                System.out.println("connection: onFailure。 value=" + value);
            }
        });

        connection.connect(new Callback<Void>() {

            @Override
            public void onSuccess(Void value) {
                System.out.println("connect: onSuccess");

                byte[] payload = "上有天堂，下有苏杭".getBytes();
                connection.publish("tio1", payload, QoS.EXACTLY_ONCE, false, new Callback<Void>() {

                    @Override
                    public void onSuccess(Void value) {
                        System.out.println("publish: onSuccess");

                        connection.disconnect(new Callback<Void>() {

                            @Override
                            public void onSuccess(Void value) {
                                System.out.println("disconnect: onSuccess");
                            }

                            @Override
                            public void onFailure(Throwable value) {
                                System.out.println("disconnect: onFailure。 value=" + value);
                            }
                        });
                    }

                    @Override
                    public void onFailure(Throwable value) {
                        System.out.println("publish: onFailure。 value=" + value);
                    }
                });
                //

            }

            @Override
            public void onFailure(Throwable value) {
                System.out.println("connection: onFailure。 value=" + value);
            }
        });
```

服务器端
-------

```java
MQTT mqtt = new MQTT();
        mqtt.setHost("ip", 1883);
        final CallbackConnection connection = mqtt.callbackConnection();
        connection.listener(new Listener() {

            @Override
            public void onConnected() {
                System.out.println("connection: onConnected");
            }

            @Override
            public void onPublish(UTF8Buffer topic, Buffer body, Runnable ack) {
                System.out.println("connection: onPublish。 topic=" + topic + ", body=" + new String(body.toByteArray()));

                ack.run();
            }

            @Override
            public void onDisconnected() {
                System.out.println("connection: onDisconnected");
            }

            @Override
            public void onFailure(Throwable value) {
                System.out.println("connection: onFailure。 value=" + value);
            }
        });

        connection.connect(new Callback<Void>() {

            @Override
            public void onSuccess(Void value) {
                System.out.println("connect: onSuccess");

                connection.subscribe(new Topic[] { new Topic(UTF8Buffer.utf8("tio1"), QoS.EXACTLY_ONCE) }, new Callback<byte[]>() {

                    @Override
                    public void onSuccess(byte[] value) {
                        System.out.println("subscribe: onSuccess。 value=" + new String(value));
                    }

                    @Override
                    public void onFailure(Throwable value) {
                        System.out.println("subscribe: onFailure。 value=" + value);
                    }
                });
            }

            @Override
            public void onFailure(Throwable value) {
                System.out.println("connect: onFailure。 value=" + value);
            }
        });
```
