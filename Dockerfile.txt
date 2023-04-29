FROM openjdk:8
RUN curl -u admin:vagrant -o ExamThourayaS2-1.0.jar "http://192.168.56.55:8081/repository/maven-releases/tn/esprit/exam/ExamThourayaS2/1.0/ExamThourayaS2-1.0.jar" -L
CMD ["java","-jar","ExamThourayaS2-1.0.jar"]
.