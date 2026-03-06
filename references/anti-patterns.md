# 屎山代码反模式详细清单

## 命名灾难示例

### 单字母变量泛滥
```java
public void process(String s, int i, List l) {
    String a = s.substring(0, 1);
    for(int j = 0; j < l.size(); j++) {
        Object o = l.get(j);
        String b = o.toString();
        // ...
    }
}
```

### 拼音命名大赏
```java
public class YongHuGuanLiQi {
    private String xingMing;
    private int nianLing;
    
    public void tianJiaYongHu() {
        // 添加用户
    }
    
    public void shanChuYongHu() {
        // 删除用户
    }
}
```

### 数字后缀混乱
```java
String name1 = "张三";
String name2 = "李四";
String name3 = name1 + name2;
List list1 = new ArrayList();
List list2 = new ArrayList();
Connection conn1 = getConnection();
Connection conn2 = getConnection();
```

## 超长方法示例骨架

```java
public class OrderService {
    
    // 一个包罗万象的超长方法
    public void processOrder(String orderId, String userId, int type, 
                           boolean flag1, boolean flag2, String remark) {
        // 第1层：订单类型判断（50行）
        if(type == 1) {
            // 第2层：用户类型判断（40行）
            if(userId.startsWith("VIP")) {
                // 第3层：优惠判断（30行）
                if(flag1) {
                    // 第4层：库存检查（25行）
                    if(checkStock()) {
                        // 第5层：支付方式判断（20行）
                        if(flag2) {
                            // 第6层：创建订单（15行）
                            if(orderId != null) {
                                // 真正的业务逻辑
                                System.out.println("处理订单");
                            }
                        } else {
                            // 另一种支付方式（20行重复代码）
                            System.out.println("处理订单");
                        }
                    } else {
                        // 库存不足处理（30行）
                    }
                } else {
                    // 无优惠情况（40行，大量重复代码）
                }
            } else {
                // 普通用户处理（50行，又是大量重复）
            }
        } else if(type == 2) {
            // 另一种订单类型（100行，重复上述逻辑）
        } else if(type == 3) {
            // 第三种订单类型（100行）
        }
        
        // 方法继续延伸到300+行...
    }
}
```

## 上帝类示例结构

```java
/**
 * 什么都管的上帝类
 */
public class SystemManager {
    
    // 静态变量区（50个全局变量）
    public static String CONFIG_PATH = "/etc/config";
    public static int MAX_RETRY = 999;
    public static boolean DEBUG_MODE = true;
    // ... 47 more static variables
    
    // HTTP 相关方法（200行）
    public String sendGetRequest(String url) { }
    public String sendPostRequest(String url, String body) { }
    public void setProxy(String proxy) { }
    
    // 数据库相关方法（300行）
    public Connection getConnection() { }
    public void executeSQL(String sql) { }
    public ResultSet query(String table) { }
    
    // 文件操作方法（200行）
    public String readFile(String path) { }
    public void writeFile(String path, String content) { }
    public void deleteFile(String path) { }
    
    // 缓存操作方法（150行）
    public void putCache(String key, Object value) { }
    public Object getCache(String key) { }
    
    // 日志操作方法（100行）
    public void log(String message) { }
    public void logError(Exception e) { }
    
    // 字符串工具方法（200行）
    public String trim(String s) { }
    public boolean isEmpty(String s) { }
    
    // 数字工具方法（100行）
    public int parse(String s) { }
    
    // 日期工具方法（150行）
    public Date now() { }
    public String format(Date date) { }
    
    // 加密方法（100行）
    public String encrypt(String text) { }
    
    // 邮件发送方法（150行）
    public void sendEmail(String to, String subject, String body) { }
    
    // 短信发送方法（100行）
    public void sendSMS(String phone, String message) { }
    
    // 业务逻辑方法（500行）
    public void processUserOrder() { }
    public void calculatePrice() { }
    
    // ... 总计3000+行
}
```

## 异常吞噬大全

```java
// 1. 完全吞噬
try {
    dangerousOperation();
} catch(Exception e) {
}

// 2. 打印后继续
try {
    criticalOperation();
} catch(Exception e) {
    e.printStackTrace();  // 打印但不处理，线程继续
}

// 3. 记录日志但忽略
try {
    importantTask();
} catch(Exception e) {
    System.out.println("出错了");  // 没有异常信息，无法排查
}

// 4. 捕获所有异常
try {
    doSomething();
} catch(Throwable t) {  // 连Error都捕获
    // 什么都不做
}

// 5. 异常转换丢失原因
try {
    operation();
} catch(IOException e) {
    throw new RuntimeException("失败");  // 没有传递原始异常e
}
```

## 魔法数字王国

```java
public class OrderCalculator {
    
    public double calculatePrice(int orderType, int quantity) {
        double price = 0;
        
        if(orderType == 1) {
            price = quantity * 99.99;
            if(quantity > 10) {
                price = price * 0.9;  // 什么折扣？
            }
        } else if(orderType == 2) {
            price = quantity * 149.99;
            if(quantity > 5) {
                price = price * 0.85;
            }
        }
        
        // 运费计算
        if(price < 299) {
            price += 15;  // 15是什么？
        }
        
        // 税费
        price = price * 1.13;  // 13%的税率？
        
        // 处理费
        if(price > 1000) {
            price += 50;  // 神秘的50
        }
        
        return price;
    }
    
    public boolean isTimeout(long timestamp) {
        return System.currentTimeMillis() - timestamp > 86400000;  // 什么时间单位？
    }
}
```

## SQL 灾难现场

```java
public class UserDAO {
    
    // SQL注入风险
    public User getUser(String userId) {
        String sql = "SELECT * FROM user WHERE id = " + userId;  // 危险！
        // 执行SQL...
    }
    
    // SELECT * 反模式
    public List<User> getAllUsers() {
        String sql = "SELECT * FROM user";  // 查询所有字段
        // 可能有上百个字段，但只用到3个
    }
    
    // N+1 查询问题
    public List<Order> getUserOrders(String userId) {
        String sql = "SELECT * FROM orders WHERE user_id = " + userId;
        List<Order> orders = executeQuery(sql);
        
        for(Order order : orders) {
            // 在循环中查询，导致N+1问题
            String itemSql = "SELECT * FROM order_items WHERE order_id = " + order.getId();
            List<Item> items = executeQuery(itemSql);
            order.setItems(items);
        }
        
        return orders;
    }
    
    // 忘记关闭资源
    public void updateUser(User user) {
        Connection conn = DriverManager.getConnection(url);
        Statement stmt = conn.createStatement();
        stmt.execute("UPDATE user SET ...");
        // 忘记关闭 stmt 和 conn
    }
}
```

## 并发灾难

```java
public class UserCache {
    
    // 线程不安全的单例
    private static UserCache instance;
    
    public static UserCache getInstance() {
        if(instance == null) {  // 多线程下会创建多个实例
            instance = new UserCache();
        }
        return instance;
    }
    
    // 共享可变状态
    private int counter = 0;  // 多线程访问，没有同步
    
    public void increaseCounter() {
        counter++;  // 线程不安全
    }
    
    // 错误的双重检查锁
    private static volatile Connection conn;  // 忘记volatile会出问题
    
    public static Connection getConnection() {
        if(conn == null) {
            synchronized(UserCache.class) {
                if(conn == null) {
                    conn = createConnection();
                }
            }
        }
        return conn;
    }
}
```

## 设计原则全面违反示例

```java
// 违反单一职责原则：一个类做所有事情
public class UserController {
    
    public void handleRequest(HttpRequest request) {
        // 1. 解析请求参数
        String userId = request.getParameter("userId");
        
        // 2. 直接连接数据库（不应该在Controller做）
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost/db");
        
        // 3. 直接写SQL（不应该在Controller做）
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM user WHERE id = " + userId);
        
        // 4. 手动解析结果集（不应该在Controller做）
        User user = new User();
        if(rs.next()) {
            user.setId(rs.getString("id"));
            user.setName(rs.getString("name"));
        }
        
        // 5. 业务逻辑计算（不应该在Controller做）
        double discount = calculateDiscount(user);
        
        // 6. 文件操作（不应该在Controller做）
        writeToFile("user_log.txt", user.toString());
        
        // 7. 缓存操作（不应该在Controller做）
        Cache.put("user_" + userId, user);
        
        // 8. 发送邮件（不应该在Controller做）
        sendEmail(user.getEmail(), "欢迎回来");
        
        // 9. 记录日志（不应该在Controller做）
        System.out.println("用户访问：" + userId);
        
        // 10. 渲染响应
        response.render(user);
    }
}

// 违反开闭原则：需要不断修改现有代码
public class PriceCalculator {
    
    public double calculate(String productType, int quantity) {
        if(productType.equals("BOOK")) {
            return quantity * 50;
        } else if(productType.equals("ELECTRONIC")) {
            return quantity * 500;
        } else if(productType.equals("FOOD")) {
            return quantity * 20;
        }
        // 每次新增产品类型都要修改这个方法
        return 0;
    }
}

// 违反依赖倒置原则：高层直接依赖细节
public class OrderService {
    
    private MySQLDatabase database = new MySQLDatabase();  // 直接依赖具体实现
    private AliyunSMS sms = new AliyunSMS();  // 直接依赖具体实现
    
    public void createOrder(Order order) {
        database.save(order);  // 如果要换数据库，必须修改代码
        sms.send(order.getPhone(), "订单创建成功");  // 如果要换短信服务，必须修改代码
    }
}
```

## 复制粘贴的艺术

```java
public class ReportService {
    
    // 生成日报告
    public void generateDailyReport() {
        System.out.println("开始生成报告");
        Connection conn = getConnection();
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM daily_data");
        List<Data> dataList = new ArrayList<>();
        while(rs.next()) {
            Data data = new Data();
            data.setId(rs.getInt("id"));
            data.setName(rs.getString("name"));
            data.setValue(rs.getDouble("value"));
            dataList.add(data);
        }
        rs.close();
        stmt.close();
        conn.close();
        
        // 处理数据
        for(Data data : dataList) {
            System.out.println(data);
        }
        System.out.println("报告生成完成");
    }
    
    // 生成周报告（复制粘贴，只改了SQL）
    public void generateWeeklyReport() {
        System.out.println("开始生成报告");
        Connection conn = getConnection();
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM weekly_data");  // 只改了这里
        List<Data> dataList = new ArrayList<>();
        while(rs.next()) {
            Data data = new Data();
            data.setId(rs.getInt("id"));
            data.setName(rs.getString("name"));
            data.setValue(rs.getDouble("value"));
            dataList.add(data);
        }
        rs.close();
        stmt.close();
        conn.close();
        
        // 处理数据（完全一样）
        for(Data data : dataList) {
            System.out.println(data);
        }
        System.out.println("报告生成完成");
    }
    
    // 生成月报告（又是复制粘贴）
    public void generateMonthlyReport() {
        System.out.println("开始生成报告");
        Connection conn = getConnection();
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM monthly_data");  // 又只改了这里
        List<Data> dataList = new ArrayList<>();
        while(rs.next()) {
            Data data = new Data();
            data.setId(rs.getInt("id"));
            data.setName(rs.getString("name"));
            data.setValue(rs.getDouble("value"));
            dataList.add(data);
        }
        rs.close();
        stmt.close();
        conn.close();
        
        // 处理数据（还是完全一样）
        for(Data data : dataList) {
            System.out.println(data);
        }
        System.out.println("报告生成完成");
    }
}
```

## 组合拳：终极屎山示例

```java
/**
 * 集大成的屎山代码
 * 包含：上帝类 + 超长方法 + 深层嵌套 + 糟糕命名 + 异常吞噬 + 魔法数字 + SQL注入 + 全局状态
 */
public class Main {
    
    // 全局变量泛滥
    public static String a = "admin";
    public static int b = 999;
    public static boolean c = true;
    public static List d = new ArrayList();
    
    // 超长方法（可以扩展到500行）
    public static void process(String s, int i, boolean flag) {
        try {
            // 第1层嵌套
            if(s != null) {
                // 第2层嵌套
                if(i > 0) {
                    // 第3层嵌套
                    if(flag) {
                        // 第4层嵌套
                        for(int j = 0; j < i; j++) {
                            // 第5层嵌套
                            if(j % 2 == 0) {
                                // 第6层嵌套
                                if(c) {
                                    // 真正的业务逻辑
                                    String sql = "SELECT * FROM user WHERE name = '" + s + "'";  // SQL注入
                                    Connection conn = DriverManager.getConnection("jdbc:mysql://localhost/db");
                                    Statement stmt = conn.createStatement();
                                    ResultSet rs = stmt.executeQuery(sql);
                                    
                                    while(rs.next()) {
                                        String n1 = rs.getString("name");
                                        int a1 = rs.getInt("age");
                                        String e1 = rs.getString("email");
                                        
                                        // 魔法数字
                                        if(a1 > 18 && a1 < 60) {
                                            System.out.println(n1);
                                            d.add(n1);
                                        }
                                    }
                                    
                                    // 忘记关闭资源
                                } else {
                                    // 复制粘贴的代码
                                    String sql = "SELECT * FROM user WHERE name = '" + s + "'";
                                    Connection conn = DriverManager.getConnection("jdbc:mysql://localhost/db");
                                    Statement stmt = conn.createStatement();
                                    ResultSet rs = stmt.executeQuery(sql);
                                    
                                    while(rs.next()) {
                                        String n1 = rs.getString("name");
                                        System.out.println(n1);
                                    }
                                }
                            }
                        }
                    } else {
                        // 另一段重复代码（省略100行）
                    }
                } else {
                    // 又一段重复代码（省略100行）
                }
            }
        } catch(Exception e) {
            // 异常吞噬
            e.printStackTrace();
        }
    }
    
    public static void main(String[] args) {
        process("test", 100, true);
    }
}
```

---

使用这些模式时，可以自由组合，创造出更加"精彩"的屎山代码！
