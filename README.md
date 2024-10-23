import java.sql.*;
import java.util.Scanner;

public class UserManagement {
    
    // Method to connect to database
    private static Connection connect() {
        String url = "jdbc:mysql://localhost:3306/user_management";
        String user = "root"; // Change to your DB username
        String password = ""; // Change to your DB password
        Connection conn = null;
        try {
            conn = DriverManager.getConnection(url, user, password);
        } catch (SQLException e) {
            System.out.println(e.getMessage());
        }
        return conn;
    }
    
    // Insert user into database
    public static void insertUser(String username, double balance) {
        String sql = "INSERT INTO users(username, balance) VALUES(?,?)";
        try (Connection conn = connect();
             PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setString(1, username);
            pstmt.setDouble(2, balance);
            pstmt.executeUpdate();
            System.out.println("User added successfully!");
        } catch (SQLException e) {
            System.out.println(e.getMessage());
        }
    }
    
    // Update user balance
    public static void updateUserBalance(int id, double balance) {
        String sql = "UPDATE users SET balance = ? WHERE id = ?";
        try (Connection conn = connect();
             PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setDouble(1, balance);
            pstmt.setInt(2, id);
            pstmt.executeUpdate();
            System.out.println("User balance updated successfully!");
        } catch (SQLException e) {
            System.out.println(e.getMessage());
        }
    }
    
    // Delete user
    public static void deleteUser(int id) {
        String sql = "DELETE FROM users WHERE id = ?";
        try (Connection conn = connect();
             PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setInt(1, id);
            pstmt.executeUpdate();
            System.out.println("User deleted successfully!");
        } catch (SQLException e) {
            System.out.println(e.getMessage());
        }
    }
    
    // Fetch all users
    public static void fetchUsers() {
        String sql = "SELECT * FROM users";
        try (Connection conn = connect();
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery(sql)) {
            while (rs.next()) {
                System.out.println(rs.getInt("id") + " - " +
                                   rs.getString("username") + " - " +
                                   rs.getDouble("balance"));
            }
        } catch (SQLException e) {
            System.out.println(e.getMessage());
        }
    }

    // Main function to drive the program
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean running = true;
        
        while (running) {
            System.out.println("\n1. Add User\n2. Update Balance\n3. Delete User\n4. View Users\n5. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();
            
            switch (choice) {
                case 1:
                    System.out.print("Enter username: ");
                    String username = scanner.next();
                    System.out.print("Enter balance: ");
                    double balance = scanner.nextDouble();
                    insertUser(username, balance);
                    break;
                case 2:
                    System.out.print("Enter user ID: ");
                    int userId = scanner.nextInt();
                    System.out.print("Enter new balance: ");
                    double newBalance = scanner.nextDouble();
                    updateUserBalance(userId, newBalance);
                    break;
                case 3:
                    System.out.print("Enter user ID to delete: ");
                    int deleteId = scanner.nextInt();
                    deleteUser(deleteId);
                    break;
                case 4:
                    fetchUsers();
                    break;
                case 5:
                    running = false;
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid option, try again.");
            }
        }
        
        scanner.close();
    }
}

public class BreakContinueExample {
    public static void main(String[] args) {
        for (int i = 1; i <= 10; i++) {
            if (i == 5) {
                System.out.println("Skipping number 5");
                continue; // Skip iteration when i == 5
            }
            if (i == 8) {
                System.out.println("Breaking the loop at number 8");
                break; // Exit loop when i == 8
            }
            System.out.println(i);
        }
    }
}

public class BreakContinueWhileExample {
    public static void main(String[] args) {
        int i = 1;
        while (i <= 10) {
            if (i == 3) {
                System.out.println("Skipping number 3");
                i++;
                continue; // Skip the rest of the loop when i == 3
            }
            if (i == 7) {
                System.out.println("Breaking the loop at number 7");
                break; // Exit loop when i == 7
            }
            System.out.println(i);
            i++;
        }
    }
}
