```markdown
# CRM System using Neo4j

This project implements a basic **Customer Relationship Management (CRM)** system using a **Neo4j** graph database with Python. It models customers, products, and purchases as nodes and their interactions as relationships using Neo4j’s graph structure.

## Features

- Add and manage customers and products.
- Record purchases made by customers.
- Retrieve all products purchased by a customer.
- Retrieve all customers who purchased a specific product.

## Technologies Used

- **Python**
- **Neo4j** Graph Database
- **Neo4j Python Driver** for connecting to the Neo4j database.

## Requirements

- Python 3.x
- Neo4j installed locally or remotely.
- Python packages:
  - neo4j: `pip install neo4j`

## Installation

1. **Clone the repository**:

    ```bash
    git clone https://github.com/matt7salomon/Customer_Relationship_Management_Neo4J_Graph_Database
    cd Customer_Relationship_Management_Neo4J_Graph_Database
    ```

2. **Set up Neo4j**:

    - Install [Neo4j](https://neo4j.com/download/) and run the database.
    - Create a user and password for your Neo4j instance.

3. **Install Python dependencies**:

    ```bash
    pip install neo4j
    ```

4. **Update Connection Details**:

    Update the connection details in `crm_neo4j.py` for your Neo4j instance:

    ```python
    crm = CRMNeo4j("bolt://localhost:7687", "neo4j", "password")
    ```

## How to Use

1. **Initialize the CRM**:
    ```python
    crm = CRMNeo4j("bolt://localhost:7687", "neo4j", "your_password")
    ```

2. **Add customers**:
    ```python
    crm.add_customer("CUST001", "John Doe", "john@example.com")
    crm.add_customer("CUST002", "Jane Smith", "jane@example.com")
    ```

3. **Add products**:
    ```python
    crm.add_product("PROD001", "Laptop", 999.99)
    crm.add_product("PROD002", "Smartphone", 499.99)
    ```

4. **Record a purchase**:
    ```python
    crm.add_purchase("CUST001", "PROD001", "2024-01-10")
    crm.add_purchase("CUST002", "PROD002", "2024-01-15")
    ```

5. **Retrieve customer purchases**:
    ```python
    purchases = crm.get_customer_purchases("CUST001")
    print(f"John's Purchases: {purchases}")
    ```

6. **Retrieve product's customers**:
    ```python
    customers = crm.get_product_customers("PROD002")
    print(f"Smartphone Customers: {customers}")
    ```

7. **Close the connection** when done:
    ```python
    crm.close()
    ```

## CRM Model

### Nodes:

- **Customer**: Represents a customer with properties:
  - `customer_id`: A unique ID for the customer.
  - `name`: Name of the customer.
  - `email`: Email of the customer.
  
- **Product**: Represents a product with properties:
  - `product_id`: A unique ID for the product.
  - `name`: Name of the product.
  - `price`: Price of the product.

### Relationships:

- **PURCHASED**: Represents a customer purchasing a product. This relationship can have additional attributes such as the `date` of purchase.

### Cypher Queries:

- **Create Customer**:
  ```cypher
  CREATE (c:Customer {customer_id: $customer_id, name: $name, email: $email})
  RETURN c
  ```

- **Create Product**:
  ```cypher
  CREATE (p:Product {product_id: $product_id, name: $name, price: $price})
  RETURN p
  ```

- **Record Purchase**:
  ```cypher
  MATCH (c:Customer {customer_id: $customer_id}), (p:Product {product_id: $product_id})
  CREATE (c)-[:PURCHASED {date: $date}]->(p)
  RETURN c, p
  ```

## Future Enhancements

- Add features for managing orders, invoices, and customer feedback.
- Integrate a web interface for better interaction with the CRM system.
- Add more complex relationship attributes like quantity and discounts.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
```
