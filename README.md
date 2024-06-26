<div>
    <div>
        <h1>Cloud Vendor Service</h1>
        <p>I have created a project named Cloud Vendor API with Spring Boot which will provide cloud vendor information service. </p>
    </div>
    <div>
        <h3>The project Architecture is:</h3>
        <p>REST CLIENT ---(CRUD)---- Controller Layer  Business/Service Layer  Database/Repository Layer  Database</p>
        <ul>
            <li> REST CLIENT: Any application can be called as rest client which can send rest request and get the response back. Like postman, Browser Window etc. It interacts with Controller Layer through CRUD operations.<br><br></li>
            <li>Controller Layer:  It will be interacting with REST CLIENT with CRUD operations. This layer is responsible to accept rest request and response back. All the rest api’s exposure will happened here. It will interact with Business/Service Layer.<br><br></li>
            <li>Business/Service Layer: Any business logic which we want to write for our project should go there. It will interact with Repository/Database Layer.<br><br></li>
            <li>Repository/Database Layer:</> Any database related operations will be in this layer. It will interact with the database.<br><br></li>
            <li>Database:</> It will perform the operations whatever is triggered by repository layer. Once that operation is performed, database will then the response back to repository layer.<br></li>
        </ul>
            <p>Repository layer will send the response back to the service layer. And Service layer will send the response back to the controller layer. Controller layer will response back to the rest client.
            That how entire functionality works.</p>
    </div>
    <div>
        <h3> Starting Project</h3>
        <ul>
            <li>Starting the project with Spring Initializer.</li>
            <li>Added the dependency 1. Spring Web, 2. JPA, 3. MySQL</li>
            <li>Created application.yaml in resource package where mysql database connector is configured.</li>
        </ul>
        <br>
    </div>
    <div>
        <h3>Class Description</h3>
        <ul>
            <li>
                <b>Create CloudVendor class in Model package.</b><br>
                <p>Here we created the fields like vendorId, vendorName, vendorAddress and vendorPhoneNumber with each String type. 
                Created a constructor with these parameters.<br>
                Add Setter and getter method for each field.<br></p>
                Used some annotations. Like
                <ol type="1">
                    <li> @Entity:  It marks the class as an entity indicating that instances of this class will be persisted to the database.</li>
                    <li> @Table: Table(name = “table name”). It specifies the name of the database table to which this entity is mapped.</li>
                    <li> @Id: It is used to specify the primary key. Here we make vendorId as Primary key.</li>
                </ol>
                <br><br>
            </li>
            <li>
                <b>Create CloudVendorController in Controller package.</b><br>
                <p>It will work as Controller layer. <br>
                Used some annotations. Like
                <ol type="1">
                    <li> @RestController: Used to define a controller class in spring MVC(model view controller) that handles http request and automatically serializes the return value int JSON or XML and write the response back to the HttpServletResponse Object.</li>
                    <li> @RequestMapping: It maps http request to handler methods of this controller class. All handler methods int this class are related to the base path “/cloudvendor”</li>
                </ol>
                <p>Here “privet final CloudVendorService cloudVendorService” field hold an interface which provides methods for interacting with “CloudVendor” entities in the database.
                “final” means it initializes only once and cannot be reassigned.
                Lastly added a constructor and CRUD handler which fetch, persist and delete data in database.
                </p><br>
            </li>
            <li>
                <b>Create CloudVendorController in Controller package.</b><br>
                <p>This interface outlines the contract for managing cloud vendor entities in the application. It defines a set of operations including CRUD.</p><br>
            </li>
            <li>
                <b>Create CloudVendorRepository class in repository package</b><br>
                <p>It extends JPA repository interface which provides standard CRUD operations for the CloudVendor entity type.<br>
                Here parameter “CloudVendor” refers to the entity type manage by this repository. And “String” is the type of primary key of the CloudVendor entity.<br>
                It inherits various methods form JpaRepository such as Save, findById, findAll, delete etc.
                </p><br>
            </li>
            <li>
                Create CloudVendorServiceImplementation class in service.implementation package.<br>
                <p>Here, Service annotation is a part of the spring framework and it indicate that this class is a service component that should be picked up during components scanning and managed by the spring container.<br>
                This class implements all the methods of CloudVendorService interface,<br>
                It provides implementations for CRUD operations on cloud vendor by interacting with the CloudVendorReporsitory. This class is managed by the spring container and is available for use throughout the application where CloudVendorService is required.
                </p><br>
            </li>
            <li>
                <b>Lastly, Exception Handling:</b><br>
                <p>It handled by three steps.</p>
                <ol type="1">
                    <li> Create CloudVendorNotFoundException class which extends RuntimeException so that it can be recognize as Exception class or making it an unchecked exception. There will be two constructors. One constructor with only showing the error message, another will show the message with the cause of the exception.<br></li>
                    <li> Create class CloudVendorException with three field (message, cause, HTTP stutus) that will show the client. Create constructor with these fields and getter method for each.<br></li>
                    <li> Add handler to handle this exception. For this, create CloudVendorExceptionHandler class which include a handler method and the return type of this method will be ResponseEntity"Object".<br>
                    This method will have cloudVendorNotFoundException instance.<br><br>
                    In the implementation of this handler method two important things will be going.<br>
                        <ol>
                            <li>We will create a payload (CloudVendorException cloudVendorException = new CloudVendorException(message, cause, and status).<br></li>
                            <li>Return back with the help of response entities. Two argument will be returned. One is cloudVendorException which we create in the payload and another is HTTP status.</li>
                        </ol>
                    </li>
                    <p>This class will have ExceptionHandler annotation which tells that it is going to handle all exceptions of the project. This annotation will have value = {cloudVendorNotFound.class}. It means, it contains the list of exceptions.<br>
                    Another annotation is “ControllerAdvice” which used to define global exception handling for controllers in the application. It allows centralized exception handling across all containers.
                    </p>
                </ul>
                <p>Now exception handle is ready. It can be used anywhere that needed. Like, we can use it in CloudVendorServiceImplentation class where single query is called.</p>
            </li>
        </ul>
    </div>
</div>


