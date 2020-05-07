Normalization Notes:

WARNING: We made mistakes (and fixed them as we went) while working through this exercise. If you do not watch the video then this exercise will not make sense. This is the kind of thing where you SHOULD be able to go through the steps once and get it right, but USUALLY people realize the screwed up on 3NF and have to go back to 2NF.

1) Reduce redundencies
Store the data in one place and only one place

2) Reduce anomalies
If I update, insert, or delete a parent record, what happens to the child records? Is data integrity and consistency maintained?
    a) update anomalies
    b) insert anomalies
    c) delete anomalies

Data can exist in the following states:
0NF     - completely un-normalized data.
1NF     - First Normal Form
2NF     - Second Normal Form
3NF     - Third Normal Form
BCNF    - Boyce-Codd Normal Form
4NF     - Fourth Normal Form
DKNF    - Domain-Key Normal Form

We will go through 0NF to 3NF. Each Normal Form represents a set of rules that have been applied to the data. 1NF, 2NF, and 3NF are based on E.F. Codd's original research which is summarized in Codd's Law. BCNF is a revision of 3NF (not a heirarchal continuation from 3NF). DKNF is based on research by Fagin (1981) but there is no defined method or step-by-step procedure for consistently creating a DKNF normalized database. Most folks just use 3NF.

CODD'S Law
The Key (1NF)
The Whole Key (2NF)
And Nothing But The Key (3NF)

Normalizing data will inherently increase the number of tables and increases performance costs. But it also makes data more maintainable and less prone to errors. The trade-off is usally worth it. There are alternatives to normalized data (called de-normalized data). There are also alternatives to relational databases like GraphQL, and other No-SQL databases. These are typically faster, but most enterprises will use a RDBMS with normalized data.

Primary Key
    Uniquely identifies a row in a table. Every table has a PK. Usually one column but can be made of multiple columns. Aaron likes to use nothing but GUIDs whenever possible because of how unique they are (https://www.guidgenerator.com/online-guid-generator.aspx)
Foreign Key
    Defines a relationship between two tables.

Many-to-Many Relationships and Composite Keys
    Resolved with Associative Entities that typically have PKs made out of FKs that are actually the PKs from each of the tables. The Primary Key would be a type of key called a Composite Key - A key that is composed of multiple attributes.

0NF (https://www.kaggle.com/kyanyoga/sample-sales-data#sales_data_sample.csv PUBLIC DOMAIN)

Delete all 'calculated fields' (fields which are basically another column with math).

ORDERNUMBER, QUANTITYORDERED, PRICEEACH, ORDERLINENUMBER, SALES, ORDERDATE, STATUS, QTR_ID, MONTH_ID, YEAR_ID, PRODUCTLINE, MSRP, PRODUCTCODE, CUSTOMERNAME, PHONE, ADDRESS

1NF - THE KEY
    Has 2 rules:
        a) All data must be atomic
        b) Isolate all repeating database

*Weird Business Rule: All orders must have at least 2 customers (Our site is called "Halfsies" where two people go halfsies on a purchase)

(PK)ORDER_NUMBER, (FK)CUSTOMER_ID1, (FK)CUSTOMER_ID2, QUANTITY_ORDERED, PRICE_EACH, ORDER_LINE_NUMBER, ORDER_DATE, SHIPPING_STATUS, QUARTER_ID, PRODUCT_LINE, MANUFACTURER_SUGGESTED_RETAIL_PRICE, PRODUCT_CODE, ADDRESS_LINE_1, ADDRESS_LINE_2, ADDRESS_LINE_3, ADDRESS_LINE_4, CITY, PROVINCE_STATE, COUNTRY, POSTAL_ZIP_CODE, CARE_OF, UNIT_NUMBER, PO_BOX

(PK)CUSTOMER_ID, CUSTOMER_LAST_NAME, CUSTOMER_MIDDLE_INITIAL, CUSTOMER_FIRST_NAME, CUSTOMER_TITLE, CUSTOMER_NAME_SUFFIX, PHONE

2NF - THE WHOLE KEY
    1 rule:
    The attributes must depend on all parts of composite primary keys.
    If you do not have a composite primary key in any of your tables, then do nothing.

(PK)ORDER_NUMBER, (FK)CUSTOMER_ID1, (FK)CUSTOMER_ID2, QUANTITY_ORDERED, PRICE_EACH, ORDER_DATE, SHIPPING_STATUS, QUARTER_ID, PRODUCT_LINE, MANUFACTURER_SUGGESTED_RETAIL_PRICE, PRODUCT_CODE, ADDRESS_LINE_1, ADDRESS_LINE_2, ADDRESS_LINE_3, ADDRESS_LINE_4, CITY, PROVINCE_STATE, COUNTRY, POSTAL_ZIP_CODE, CARE_OF, UNIT_NUMBER, PO_BOX

(PK)CUSTOMER_ID, CUSTOMER_LAST_NAME, CUSTOMER_MIDDLE_INITIAL, CUSTOMER_FIRST_NAME, CUSTOMER_TITLE, CUSTOMER_NAME_SUFFIX, PHONE

(PK FK)ORDER_NUMBER,(PK FK)PRODUCT_CODE, ORDER_LINE_NUMBER

3NF - NOTHING BUT THE KEY
    1 rule:
    A non-key attribute cannot fully depend on another non-key attribute.

(PK)ORDER_NUMBER, (FK)CUSTOMER_ID1, (FK)CUSTOMER_ID2, (FK)PRODUCT_CODE, (FK)ADDRESS_ID, (FK)QUARTER_ID, QUANTITY_ORDERED, ORDER_DATE, SHIPPING_STATUS 

(PK)ADDRESS_ID, ADDRESS_LINE_1, ADDRESS_LINE_2, ADDRESS_LINE_3, ADDRESS_LINE_4, CITY, PROVINCE_STATE, COUNTRY, POSTAL_ZIP_CODE, CARE_OF, UNIT_NUMBER, PO_BOX

(PK)CUSTOMER_ID, (FK)PHONE_ID, (FK)SHIPPING_ADDRESS_ID, (FK)RESIDENTIAL_ADDRESS_ID, (FK)BILLING_ADDRESS_ID, CUSTOMER_LAST_NAME, CUSTOMER_MIDDLE_INITIAL, CUSTOMER_FIRST_NAME, CUSTOMER_TITLE, CUSTOMER_NAME_SUFFIX

(PK)PHONE_ID, PHONE_NUMBER

(PK)QUARTER_ID

(PK)PRODUCT_CODE, PRICE_EACH, PRODUCT_LINE, MANUFACTURER_SUGGESTED_RETAIL_PRICE

(PK FK)ORDER_NUMBER,(PK FK)PRODUCT_CODE, ORDER_LINE_NUMBER
