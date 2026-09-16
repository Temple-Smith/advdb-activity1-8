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
 
