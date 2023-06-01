#### Hi there! 👋
My name is「Allan Yin」 and I'm a computer science student from the University of Waterloo, in Canada. Here's some info about me!

⚡ Work experience: 
* Software Engineer intern at RBC - Full Stack development working on internal applications for RBC, focused on centralizing many company resources [Toronto. Fall 2022]
* Software Engineer intern at Bank of America (current) - Fixed income trading

🌱 Interests:
* Learning new things!
* Full-stack Development 
* Machine Learning + Deep Learning 
* Staying up to date with relevant AI research

🔭 Current Activity:
* Learning deep learning and neural networks with Keras and TensorFlow

💬 Reach me by email or LinkedIn! allanyin17@gmail.com | www.linkedin.com/in/allan-yin



### Spring Boot Introduction ###

Spring Boot is a java-based framework that follows the MVC design pattern, which stands for model view controller. While its not forced, the standard practice is to have multiple layers/Modularization. For instance, we may typically see the following format:
* **Controller**: This is the the top most level layer, and is the first to interact with the external services. 
* **Service**: When the controller receives some sort of request, will call some method defined in the service files. 
* **Repository**: This is the component that is the lowest level. In Spring Boot, we often define an interface that extends the `JPARepository`, which is an ORM. Through that, we can access to certain methods that can access the database. It's worth noting, we only need an interface, as Spring will look at the declared methods name, look for keywords, and generate the corresponding SQL statements for us. 

Spring Boot employs the IOC (Inversion of Control) principle. In traditional programming, objects are responsible for creating the managing the dependencies they need. With IOC, the control over object creation and dependency management is inverted. Instead of objects creating their dependencies, the responsibility is delegated to a separate entity known as the container or the IoC container.


This is why we create Beans, as they are managed by the Spring IOC container. This is why in Spring, we'll make certain annotations to things we want dependencies auto-injected for us, such as: 
* `@RestController`
* `@Service`
* `@Bean`
* `@Component`
* `@RabbitListener`
* `@Configuration`

In addition, there are some libraries that are good to be familiar with. In particular:
* **Jackson**: This is a library used for JSON processing. Used a lot for mapping Java objects into JSONs, and vice versa. To use it, we would use `ObjectMapper`:
```Java

ObjectMapper objectMapper = new ObjectMapper();
String JSON = objectMapper.writeValueAsString(SomeRandomDto);
logger.info(JSON) // will see the Java object in JSON format, as a string 
```
* **ModelMapper**: This is used to map one Java object to another. Is particularly useful when mapping `Entity` objects to `Dto` objects, and vice versa. 
```Java
ModelMapper modelMapper = new ModelMapper();
DestinationObject destination = modelMapper.map(source, DestinationObject.class);
```
* **Logger**: Simple tool that makes a clear and visible log in the terminal. Useful for debugging. 


Another thing that is important to know from JPA, is configuring `Entities`. When we mark a class with `@Entity`, it means it represents a table in a relational database. Below is an example: 
```Java
@Data
@NoArgsConstructor
@AllArgsConstructor
@Entity
@ToString
@Table(name = "Users")
public class User {
    @Id
    @GeneratedValue (strategy = GenerationType.IDENTITY)
    private Long id;

    @NotBlank
    private String username;

    @NotBlank
    @Email
    private String email;

    @NotBlank
    private String password;

    public User(String username, String email, String password) {
        this.username = username;
        this.email = email;
        this.password = password;
    }

    @ManyToMany(targetEntity = Role.class, cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    @JoinTable( name="user_roles", joinColumns = @JoinColumn(name = "user_id"), inverseJoinColumns = @JoinColumn(name = "role_id"))
    private Set<Role> roles = new HashSet<>();
}
```
Now, note the following about the above code:
* **@Table(name = "Users")**: This annotation is fairly obvious. It tells us this is a table with the name "Users" in the database. 
* **@Id**: This means this parameter (id) is the primary key in the table 
* **NotBlank**: Also self-explanatory. This value cannot be blank

The following annotations are and important feature in relational databases. With JPA annotations, we can specify 

Now, many of the top annotations are from a useful library called `Lombok`, which serves to avoid a lot of boilerplate code (such as getters, setters, constructors, etc). The annotations from this library include:
* **@AllArgsConstructor**
* **@NoArgsConstructor**
* **Data**





