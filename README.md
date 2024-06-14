# FinalsSQL
: Updating and Deleting
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  
  <groupId>your.group.id</groupId>
  <artifactId>your-artifact-id</artifactId>
  <version>1.0.0</version> <!-- You can set your version here -->
  
  <properties>
    <java.version>1.8</java.version> <!-- Set your desired Java version here -->
  </properties>
  
  <dependencies>
    <!-- MySQL Connector/J dependency -->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.27</version> <!-- You can specify the version of MySQL Connector/J here -->
    </dependency>
  </dependencies>
  
  <build>
    <plugins>
      <!-- Maven compiler plugin -->
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version> <!-- You can specify the version of Maven compiler plugin here -->
        <configuration>
          <source>${java.version}</source>
          <target>${java.version}</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
  
  <!-- This section is used to store Eclipse m2e settings only -->

</project>

package projects;

import java.util.Scanner;

public class ProjectsApp {
    private ProjectService projectService;
    private Projects curProject;
    private Scanner scanner;

    public ProjectsApp() {
        projectService = new ProjectService();
        scanner = new Scanner(System.in);
    }

    public void displayMenu() {
        System.out.println("Menu:");
        System.out.println("1) Create a project");
        System.out.println("2) Read project details");
        System.out.println("3) Update project details");
        System.out.println("4) Delete a project");
        System.out.println("5) Exit");
    }

    public void run() {
        int choice;
        do {
            displayMenu();
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    // Implement createProject() method
                    break;
                case 2:
                    // Implement readProjectDetails() method
                    break;
                case 3:
                    // Implement updateProjectDetails() method
                    break;
                case 4:
                    // Implement deleteProject() method
                    break;
                case 5:
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 5);
    }

    public void updateProjectDetails() {
        if (curProject == null) {
            System.out.println("\nPlease select a project.");
            return;
        }

        System.out.println("Current project details:");
        System.out.println("Project ID: " + curProject.getProjectId());
        System.out.println("Project Name: " + curProject.getProjectId());
        // Print other project details as needed


        System.out.println("Current project details:");
        System.out.println("Project ID: " + curProject.getProjectId());
        System.out.println("Project Name: " + curProject.getProjectId());
        // Print other project details as needed

        Project updatedProject = new Project();
        updatedProject.setProjectName(curProject.getProjectId());
        updatedProject.setProjectName(curProject.getProjectId());
        // Set other project details as needed

        // Get user input for updated project details
        System.out.println("\nEnter new project details:");
        System.out.print("Project Name (Enter to keep current): ");
        String projectNameInput = scanner.nextLine();
        if (!projectNameInput.isEmpty()) {
            updatedProject.setProjectName(projectNameInput);
        }
        // Set other project details as needed

        boolean success = projectService.modifyProjectDetails(updatedProject);
        if (success) {
            curProject = projectService.fetchProjectById(curProject.getProjectId());
            System.out.println("Project details updated successfully.");
        } else {
            System.out.println("Failed to update project details.");
        }
    }

    // Other methods such as createProject(), readProjectDetails(), deleteProject(), listProjects() can be implemented here

    public static void main(String[] args) {
        ProjectsApp app = new ProjectsApp();
        app.run();
    }

package projects.exception;

public class DbException extends RuntimeException {
    /**
	 * 
	 */
	private static final long serialVersionUID = 1L;

	public DbException(String message) {
        super(message);
    }

    public DbException(Throwable cause) {
        super(cause);
    }

    public DbException(String message, Throwable cause) {
        super(message, cause);
    }
}
package project.service;

import projects.Project;
import projects.exception.DbException;

import java.sql.Connection;
	import java.sql.DriverManager;
	import java.sql.PreparedStatement;
	import java.sql.SQLException;

	
	
	public class ProjectDao {
	    private static final String URL = "jdbc:mysql://localhost:3306/your_database_name";
	    private static final String USERNAME = "DanielMEDS";
	    private static final String PASSWORD = "Daisy8930!";

	    
	    public boolean modifyProjectDetails1(Project project) throws DbException {
	        String sql = "UPDATE projects SET projectName = ?, description = ?, category = ? WHERE projectId = ?";
	        try (Connection connection = DriverManager.getConnection(URL, USERNAME, PASSWORD);
	             PreparedStatement statement = connection.prepareStatement(sql)) {
	            statement.setString(1, project.getProjectName());
	            statement.setString(2, project.getDescription());
	            statement.setString(3, project.getCategory());
	            statement.setString(4, project.getProjectName());

	            int rowsUpdated = statement.executeUpdate();
	            if (rowsUpdated == 0) {
	                throw new DbException("The project with ID " + project.getProjectName() + " does not exist.");
	            }

	            return true;
	        } catch (SQLException e) {
	            throw new DbException("An error occurred while modifying project details.", e);
	        }
	    }
	
{
		// TODO Auto-generated method stub
		
	}

	public boolean modifyProjectDetails(Project project) {
		// TODO Auto-generated method stub
		return false;
	}

}
