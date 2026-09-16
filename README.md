# advdb-activity1-8
A local gym and fitness centre needs to manage its members, trainers, classes and payments. We've been hired to design a logical database model that supports these operations efficiently and accurately.

We will create an entity relationship diagram (ERD) that captures the relationships between entities (one-to-many, many-to-many, etc.), we will use LucidChart to create our diagram.

We will identify primary and foreign keys and ensure business requirements are adhered to.

Finally, we will apply normalization up to 3rd normal form to our solution to eliminate data redundancy.

Write 4–6 clear rules describing how data interacts (e.g., “Each trainer can lead multiple classes.”).
Rules on how data interacts:

1. A class can only have one trainer, but a trainer can have multiple classes (one and only one to many)
2. A class can have multiple enrollments, but an enrollment can only have one class
3. A person can either be exclusively a walk-in, a trainer, or a member.
4. The payment table is a weak entity that requires a membership to exist.
 
## Rationale 

We decided to accommodate the possibility of a trainer also being a member at the gym by implementing a partial overlapping specialization.  

We chose to make a junction table to keep track of class enrollments to minimize duplicated data and simplify queries. This table allows members to register for courses and for courses to keep track of enrolled members. 

A member type table is used to provide “member_type_id” values with a name, description, and a foreign key to reference. We did the same with membership_status. 

We have a weak entity with PAYMENT because a payment is dependent on a membership existing, and we are connecting the payment data with a member id and payment id. 

We ensure normalization to 3NF step by step, there are no values that aren’t atomic, and every non-key attribute is wholly dependent on the primary key. We reduced duplicated data and avoided anomalies with CRUD operations  

 

## Business Rules 

A `PERSON` can be either a member, trainer, or a walk in 

Every `PERSON` is classified by one `MEMBER_TYPE`, and one `MEMBER_TYPE` may have either zero, one, or many people 

A PERSON can be a `WALK_IN`. A walk-in data belongs to only one person. 

`MEMBER_SUB` and `TRAINER` are partial, overlapping specializations. A `PERSON` is not required to be either subtype and the same `PERSON` can be both a `MEMBER_SUB` and a `TRAINER` 

`WALK_IN` is stores a temp member id and visit date rather than subscription data 

A `CLASS` can only have one `TRAINER`, but a trainer can have multiple classes (one and only one to many) 

A `CLASS` can have multiple enrollments, but an enrollment can only have one class 

The `PAYMENT` table is a weak entity that requires membership to exist. 

Every `PAYMENT` must have exactly one `PAYMENT_METHOD`  

Membership expiry date cannot be earlier than join date 

`MEMBER_SUB` must have exactly one `MEMBERSHIP_STATUS`. Status can apply to zero, one or many memberships 

A `MEMBER_SUB` can make zero, one or many `PAYMENT` records. Every `PAYMENT` belongs to exactly one `MEMBER_SUB`

 

### Relationships and Cardinalities 

| Relationship | Cardinality | Description |  
| --- | --- | --- | 
| `MEMBER_TYPE` **classifies** `PERSON` | 1 : M | One member type may classify zero or many people; each person references one member type. | 
| `PERSON` → `MEMBER_SUB` / `TRAINER` | Partial, overlapping specialization | A person may be neither subtype, one subtype, or both subtypes. | 
| `PERSON` **may be a** `WALK_IN` | 1 : 0..1 | A person may have no walk-in record or one walk-in record; every walk-in belongs to one person. |  
| `MEMBERSHIP_STATUS` **sets status of** `MEMBER_SUB` | 1 : M | One status may apply to zero or many memberships; each member has one status. |  
| `MEMBER_SUB` **makes** `PAYMENT` | 1 : M | A member may make zero or many payments; each payment belongs to one member. |  
| `PAYMENT` **paid via** `PAYMENT_METHOD` | M : 1 | Every payment uses one payment method; a payment method may be used by many payments. |  
| `TRAINER` **teaches** `CLASS` | 1 : M | A trainer may teach zero or many classes; every class has one trainer. |  
| `MEMBER_SUB` **has enrollments** `CLASS_ENROLLMENT` | 1 : M | A member may have zero or many enrollments; each enrollment belongs to one member. |  
| `CLASS` **has enrollments** `CLASS_ENROLLMENT` | 1 : M | A class may have zero or many enrollments; each enrollment belongs to one class. |  
 
