# plpdart
void main() {
  // Initialize shopping cart with various items
  List<Map<String, dynamic>> cart = [
    {'name': 'Laptop', 'price': 899.99},
    {'name': 'Phone Case', 'price': 15.50},
    {'name': 'Coffee Mug', 'price': 8.99},
    {'name': 'Wireless Mouse', 'price': 25.00},
    {'name': 'Notebook', 'price': 5.99},
    {'name': 'Headphones', 'price': 79.99},
    {'name': 'USB Cable', 'price': 12.49},
    {'name': 'Stickers', 'price': 3.99},
  ];

  print('🛒 Online Shopping Cart System');
  print('=' * 40);
  
  // Display original cart
  print('\n📦 Original Cart Items:');
  displayCart(cart);
  print('Original Total: \$${calculateTotal(cart).toStringAsFixed(2)}');

  // Step 1: Filter items using anonymous function (remove items below $10)
  print('\n🔍 Step 1: Filtering items below \$10...');
  var filteredCart = cart.where((item) => item['price'] >= 10.0).toList();
  print('Items after filtering:');
  displayCart(filteredCart);

  // Step 2: Apply discount using higher-order function
  print('\n💸 Step 2: Applying 15% discount...');
  var discountedCart = applyDiscount(filteredCart, 0.15);
  print('Items after discount:');
  displayCart(discountedCart);

  // Step 3: Calculate total with optional tax
  print('\n🧮 Step 3: Calculating totals...');
  double subtotal = calculateTotal(discountedCart);
  double totalWithTax = calculateTotalWithTax(discountedCart, 0.08); // 8% tax
  
  print('Subtotal: \$${subtotal.toStringAsFixed(2)}');
  print('Total with 8% tax: \$${totalWithTax.toStringAsFixed(2)}');

  // Step 4: Apply factorial discount based on item count
  print('\n🎯 Step 4: Applying factorial discount...');
  int itemCount = discountedCart.length;
  double factorialValue = factorial(itemCount).toDouble();
  double factorialDiscount = factorialValue / 100; // Convert to percentage
  
  print('Number of items: $itemCount');
  print('Factorial of $itemCount: ${factorialValue.toInt()}');
  print('Factorial discount: ${factorialDiscount.toStringAsFixed(2)}%');
  
  double finalPrice = totalWithTax * (1 - factorialDiscount / 100);
  
  // Step 5: Display final results
  print('\n🏁 Final Results:');
  print('=' * 40);
  print('Original Total: \$${calculateTotal(cart).toStringAsFixed(2)}');
  print('After filtering: \$${calculateTotal(filteredCart).toStringAsFixed(2)}');
  print('After 15% discount: \$${subtotal.toStringAsFixed(2)}');
  print('After 8% tax: \$${totalWithTax.toStringAsFixed(2)}');
  print('Factorial discount (${factorialDiscount.toStringAsFixed(2)}%): -\$${(totalWithTax - finalPrice).toStringAsFixed(2)}');
  print('');
  print('🎉 FINAL PRICE: \$${finalPrice.toStringAsFixed(2)}');
  
  // Demonstrate additional functional programming concepts
  print('\n🔧 Additional Functional Programming Examples:');
  demonstrateAdvancedConcepts(cart);
}

// Higher-order function: Takes a function as parameter to apply discount
List<Map<String, dynamic>> applyDiscount(List<Map<String, dynamic>> items, double discountRate) {
  // Using map with anonymous function
  return items.map((item) => {
    'name': item['name'],
    'price': item['price'] * (1 - discountRate)
  }).toList();
}

// Function to calculate total using fold (functional approach)
double calculateTotal(List<Map<String, dynamic>> items) {
  return items.fold(0.0, (sum, item) => sum + item['price']);
}

// Function to calculate total with optional tax
double calculateTotalWithTax(List<Map<String, dynamic>> items, [double taxRate = 0.0]) {
  double subtotal = calculateTotal(items);
  return subtotal * (1 + taxRate);
}

// Recursive function: Calculate factorial
int factorial(int n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}

// Helper function to display cart items
void displayCart(List<Map<String, dynamic>> items) {
  for (var item in items) {
    print('  • ${item['name']}: \$${item['price'].toStringAsFixed(2)}');
  }
  print('  Items count: ${items.length}');
}

// Advanced functional programming demonstrations
void demonstrateAdvancedConcepts(List<Map<String, dynamic>> originalCart) {
  print('\n1. Chaining Operations (Fluent Interface):');
  var result = originalCart
      .where((item) => item['price'] > 10) // Anonymous function
      .map((item) => item['price']) // Anonymous function
      .reduce((a, b) => a + b); // Anonymous function
  print('   Chained total of items > \$10: \$${result.toStringAsFixed(2)}');

  print('\n2. Higher-order Function with Custom Logic:');
  var expensiveItems = filterByCondition(originalCart, (item) => item['price'] > 50);
  print('   Expensive items (>\$50):');
  for (var item in expensiveItems) {
    print('     • ${item['name']}: \$${item['price'].toStringAsFixed(2)}');
  }

  print('\n3. Recursive Price Calculation with Compound Interest:');
  double compoundPrice = calculateCompoundPrice(100.0, 0.05, 3);
  print('   \$100 with 5% compound interest for 3 periods: \$${compoundPrice.toStringAsFixed(2)}');

  print('\n4. Function Composition:');
  var composedFunction = compose(
    (x) => x * 1.1, // Add 10% markup
    (x) => x * 0.9  // Apply 10% discount
  );
  double composedResult = composedFunction(100.0);
  print('   \$100 with composed discount+markup: \$${composedResult.toStringAsFixed(2)}');
}

// Higher-order function: Filter items by custom condition
List<Map<String, dynamic>> filterByCondition(
    List<Map<String, dynamic>> items, 
    bool Function(Map<String, dynamic>) condition) {
  return items.where(condition).toList();
}

// Recursive function: Calculate compound interest
double calculateCompoundPrice(double principal, double rate, int periods) {
  if (periods <= 0) return principal;
  return calculateCompoundPrice(principal * (1 + rate), rate, periods - 1);
}

// Function composition: Combine two functions
Function compose(Function f, Function g) {
  return (x) => f(g(x));
}

// Advanced higher-order function: Apply multiple transformations
List<Map<String, dynamic>> applyTransformations(
    List<Map<String, dynamic>> items,
    List<Map<String, dynamic> Function(Map<String, dynamic>)> transformations) {
  return items.map((item) {
    var transformedItem = item;
    for (var transform in transformations) {
      transformedItem = transform(transformedItem);
    }
    return transformedItem;
  }).toList();
}
