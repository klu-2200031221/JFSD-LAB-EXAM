# JFSD-LAB-EXAM
**POM.XML**

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.klef.jfsd.exam</groupId>
  <artifactId>Labexam</artifactId>
  <version>0.0.1-SNAPSHOT</version>

  <name>Labexam</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.release>17</maven.compiler.release>
  </properties>

  <dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>org.junit</groupId>
        <artifactId>junit-bom</artifactId>
        <version>5.11.0</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
    </dependencies>
  </dependencyManagement>

  <dependencies>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter-api</artifactId>
      <scope>test</scope>
    </dependency>
    <!-- Optionally: parameterized tests support -->
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter-params</artifactId>
      <scope>test</scope>
    </dependency>
    <!-- SLF4J API -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.32</version> <!-- or latest version -->
    </dependency>

    <!-- Logback classic (SLF4J implementation) -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.6</version> <!-- or latest version -->
    </dependency>

    <!-- Other dependencies like Spring -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.20</version>
    </dependency>
    <!-- Add other Spring dependencies as needed -->

  </dependencies>

  <build>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <!-- clean lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#clean_Lifecycle -->
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.4.0</version>
        </plugin>
        <!-- default lifecycle, jar packaging: see https://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_jar_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.3.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.13.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>3.3.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-jar-plugin</artifactId>
          <version>3.4.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>3.1.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>3.1.2</version>
        </plugin>
        <!-- site lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#site_Lifecycle -->
        <plugin>
          <artifactId>maven-site-plugin</artifactId>
          <version>3.12.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-project-info-reports-plugin</artifactId>
          <version>3.6.1</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

**ApplicationContext.XML**
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Bean Definitions -->
    <bean id="employee" class="com.klef.jfsd.exam.Employee">
        <constructor-arg value="101"/>
        <constructor-arg value="John Doe"/>
        <constructor-arg value="50000"/>
        <constructor-arg value="true"/>
        <constructor-arg>
            <list>
                <value>Java</value>
                <value>Spring</value>
                <value>Hibernate</value>
            </list>
        </constructor-arg>
    </bean>

    <bean id="instructor" class="com.klef.jfsd.exam.Instructor">
        <constructor-arg value="1"/>
        <constructor-arg value="Dr. Smith"/>
        <constructor-arg value="smith@klef.com"/>
        <constructor-arg value="1234567890"/>
    </bean>

    <bean id="course" class="com.klef.jfsd.exam.Course">
        <constructor-arg value="501"/>
        <constructor-arg value="Spring Framework"/>
        <constructor-arg value="3"/>
        <constructor-arg ref="instructor"/>
    </bean>

</beans>

**ClientDemo.java**
package com.klef.jfsd.exam;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class ClientDemo {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");

        Employee employee = (Employee) context.getBean("employee");
        System.out.println("Employee Details: " + employee);

        Course course = (Course) context.getBean("course");
        System.out.println("Course Details: " + course);
    }
}

**Employee.java**

package com.klef.jfsd.exam;

import java.util.List;

public class Employee {
    private Integer employeeId;
    private String name;
    private Double salary;
    private Boolean isFullTime;
    private List<String> skills;
    public Employee(Integer employeeId, String name, Double salary, Boolean isFullTime, List<String> skills) {
        this.employeeId = employeeId;
        this.name = name;
        this.salary = salary;
        this.isFullTime = isFullTime;
        this.skills = skills;
    }
    public Integer getEmployeeId() {
        return employeeId;
    }

    public void setEmployeeId(Integer employeeId) {
        this.employeeId = employeeId;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Double getSalary() {
        return salary;
    }

    public void setSalary(Double salary) {
        this.salary = salary;
    }

    public Boolean getIsFullTime() {
        return isFullTime;
    }

    public void setIsFullTime(Boolean isFullTime) {
        this.isFullTime = isFullTime;
    }

    public List<String> getSkills() {
        return skills;
    }

    public void setSkills(List<String> skills) {
        this.skills = skills;
    }

    @Override
    public String toString() {
        return "Employee{employeeId=" + employeeId + ", name='" + name + "', salary=" + salary + ", isFullTime=" + isFullTime + ", skills=" + skills + '}';
    }
}
**Instructor.java**
package com.klef.jfsd.exam;

public class Instructor {
    private Integer instructorId;
    private String name;
    private String email;
    private String phoneNumber;
    public Instructor(Integer instructorId, String name, String email, String phoneNumber) {
        this.instructorId = instructorId;
        this.name = name;
        this.email = email;
        this.phoneNumber = phoneNumber;
    }

   
    public Integer getInstructorId() {
        return instructorId;
    }

    public void setInstructorId(Integer instructorId) {
        this.instructorId = instructorId;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }

    @Override
    public String toString() {
        return "Instructor{instructorId=" + instructorId + ", name='" + name + "', email='" + email + "', phoneNumber='" + phoneNumber + "'}";
    }
}
**Course.java**
package com.klef.jfsd.exam;

public class Course {
    private Integer courseId;
    private String courseName;
    private Integer credits;
    private Instructor instructor; 

    public Course(Integer courseId, String courseName, Integer credits, Instructor instructor) {
        this.courseId = courseId;
        this.courseName = courseName;
        this.credits = credits;
        this.instructor = instructor;
    }
    public Integer getCourseId() {
        return courseId;
    }

    public void setCourseId(Integer courseId) {
        this.courseId = courseId;
    }

    public String getCourseName() {
        return courseName;
    }

    public void setCourseName(String courseName) {
        this.courseName = courseName;
    }

    public Integer getCredits() {
        return credits;
    }

    public void setCredits(Integer credits) {
        this.credits = credits;
    }

    public Instructor getInstructor() {
        return instructor;
    }

    public void setInstructor(Instructor instructor) {
        this.instructor = instructor;
    }

    @Override
    public String toString() {
        return "Course{courseId=" + courseId + ", courseName='" + courseName + "', credits=" + credits + ", instructor=" + instructor + '}';
    }
}
