FROM adoptopenjdk/openjdk11-openj9
COPY h2-1.4.200.jar /opt
ENTRYPOINT [ "java", "-jar", "/opt/h2-1.4.200.jar", "-web", "-webAllowOthers", "-tcp", "-tcpAllowOthers", "-ifNotExists", "-baseDir", "/h2_data" ]
