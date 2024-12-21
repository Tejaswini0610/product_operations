import java.util.*;

interface ProductOperations {
    void addProduct(Product product);
    void updateStock(String productCode, int quantity);
    void removeProduct(String productCode);
    Product getProduct(String productCode);
    List<Product> getAllProducts();
}

class Product {
    private String code;
    private String name;
    private double price;
    private int stock;

    public Product(String code, String name, double price, int stock) {
        this.code = code;
        this.name = name;
        this.price = price;
        this.stock = stock;
    }

    public String getCode() {
        return code;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public int getStock() {
        return stock;
    }

    public void setStock(int stock) {
        this.stock = stock;
    }

    @Override
    public String toString() {
        return String.format("Product Code: %s, Name: %s, Price: %.2f, Stock: %d", code, name, price, stock);
    }
}

class Inventory implements ProductOperations {
    private Map<String, Product> products;

    public Inventory() {
        products = new HashMap<>();
    }

    @Override
    public void addProduct(Product product) {
        products.put(product.getCode(), product);
        System.out.println("Product added successfully: " + product);
    }

    @Override
    public void updateStock(String productCode, int quantity) {
        Product product = products.get(productCode);
        if (product != null) {
            int newStock = product.getStock() + quantity;
            if (newStock < 0) {
                System.out.println("Not enough stock to remove.");
            } else {
                product.setStock(newStock);
                System.out.println("Stock updated for " + product.getName() + ". New stock: " + newStock);
            }
        } else {
            System.out.println("Product not found.");
        }
    }

    @Override
    public void removeProduct(String productCode) {
        Product product = products.remove(productCode);
        if (product != null) {
            System.out.println("Product removed: " + product);
        } else {
            System.out.println("Product not found.");
        }
    }

    @Override
    public Product getProduct(String productCode) {
        return products.get(productCode);
    }

    @Override
    public List<Product> getAllProducts() {
        return new ArrayList<>(products.values());
    }
}

class Sales {
    private static int salesCounter = 1;
    private int saleId;
    private Date saleDate;
    private List<SaleItem> items;
    private double totalAmount;

    public Sales() {
        saleId = salesCounter++;
        saleDate = new Date();
        items = new ArrayList<>();
        totalAmount = 0.0;
    }

    public void addItem(SaleItem item) {
        items.add(item);
        totalAmount += item.getTotalPrice();
    }

    public int getSaleId() {
        return saleId;
    }

    public Date getSaleDate() {
        return saleDate;
    }

    public double getTotalAmount() {
        return totalAmount;
    }

    public List<SaleItem> getItems() {
        return items;
    }

    @Override
    public String toString() {
        return "Sale ID: " + saleId + ", Date: " + saleDate + ", Total Amount: " + totalAmount;
    }
}

class SaleItem {
    private Product product;
    private int quantity;

    public SaleItem(Product product, int quantity) {
        this.product = product;
        this.quantity = quantity;
    }

    public Product getProduct() {
        return product;
    }

    public int getQuantity() {
        return quantity;
    }

    public double getTotalPrice() {
        return product.getPrice() * quantity;
    }

    @Override
    public String toString() {
        return "Product: " + product.getName() + ", Quantity: " + quantity + ", Total: " + getTotalPrice();
    }
}

class SalesReport {
    private List<Sales> salesList;

    public SalesReport() {
        salesList = new ArrayList<>();
    }

    public void addSale(Sales sale) {
        salesList.add(sale);
    }

    public void generateReport() {
        System.out.println("\n--- Sales Report ---");
        for (Sales sale : salesList) {
            System.out.println(sale);
            for (SaleItem item : sale.getItems()) {
                System.out.println("\t" + item);
            }
        }
        System.out.println("Total Sales: " + salesList.size());
    }
}

class User {
    private String username;
    private String password;
    private Role role;

    public User(String username, String password, Role role) {
        this.username = username;
        this.password = password;
        this.role = role;
    }

    public String getUsername() {
        return username;
    }

    public String getPassword() {
        return password;
    }

    public Role getRole() {
        return role;
    }
}

enum Role {
    ADMIN, SALES, INVENTORY_MANAGER
}

class UserManagement {
    private Map<String, User> users;

    public UserManagement() {
        users = new HashMap<>();
        users.put("admin", new User("admin", "admin123", Role.ADMIN));
        users.put("sales", new User("sales", "sales123", Role.SALES));
        users.put("inventory", new User("inventory", "inventory123", Role.INVENTORY_MANAGER));
    }

    public User authenticate(String username, String password) {
        User user = users.get(username);
        if (user != null && user.getPassword().equals(password)) {
            return user;
        }
        return null;
    }

    public void addUser(User user) {
        users.put(user.getUsername(), user);
    }
}

public class InventoryManagementSystem {
    private static Scanner scanner = new Scanner(System.in);
    private static Inventory inventory = new Inventory();
    private static SalesReport salesReport = new SalesReport();
    private static UserManagement userManagement = new UserManagement();

    public static void main(String[] args) {
        User loggedInUser = login();

        if (loggedInUser != null) {
            if (loggedInUser.getRole() == Role.ADMIN) {
                adminMenu();
            } else if (loggedInUser.getRole() == Role.INVENTORY_MANAGER) {
                inventoryManagerMenu();
            } else if (loggedInUser.getRole() == Role.SALES) {
                salesMenu();
            }
        } else {
            System.out.println("Invalid credentials, exiting...");
        }
    }

    private static User login() {
        System.out.print("Enter username: ");
        String username = scanner.nextLine();
        System.out.print("Enter password: ");
        String password = scanner.nextLine();
        return userManagement.authenticate(username, password);
    }

    private static void adminMenu() {
        int choice;
        do {
            System.out.println("\n--- Admin Menu ---");
            System.out.println("1. Add Product");
            System.out.println("2. Remove Product");
            System.out.println("3. View Sales Report");
            System.out.println("4. Logout");
            System.out.print("Enter choice: ");
            choice = scanner.nextInt();
            scanner.nextLine();  // Consume newline

            switch (choice) {
                case 1:
                    addProductMenu();
                    break;
                case 2:
                    removeProductMenu();
                    break;
                case 3:
                    salesReport.generateReport();
                    break;
                case 4:
                    System.out.println("Logged out successfully.");
                    break;
                default:
                    System.out.println("Invalid choice.");
            }
        } while (choice != 4);
    }

    private static void addProductMenu() {
        System.out.print("Enter product code: ");
        String code = scanner.nextLine();
        System.out.print("Enter product name: ");
        String name = scanner.nextLine();
        System.out.print("Enter product price: ");
        double price = scanner.nextDouble();
        System.out.print("Enter product stock: ");
        int stock = scanner.nextInt();
        scanner.nextLine();  // Consume newline

        Product product = new Product(code, name, price, stock);
        inventory.addProduct(product);
    }

    private static void removeProductMenu() {
        System.out.print("Enter product code to remove: ");
        String code = scanner.nextLine();
        inventory.removeProduct(code);
    }

    private static void inventoryManagerMenu() {
        int choice;
        do {
            System.out.println("\n--- Inventory Manager Menu ---");
            System.out.println("1. Update Stock");
            System.out.println("2. View All Products");
            System.out.println("3. Logout");
            System.out.print("Enter choice: ");
            choice = scanner.nextInt();
            scanner.nextLine();  // Consume newline

            switch (choice) {
                case 1:
                    updateStockMenu();
                    break;
                case 2:
                    viewAllProducts();
                    break;
                case 3:
                    System.out.println("Logged out successfully.");
                    break;
                default:
                    System.out.println("Invalid choice.");
            }
        } while (choice != 3);
    }

    private static void updateStock
