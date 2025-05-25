## What is PostgreSQL?

PostgreSQL মুলত একটি, ওপেন-সোর্স রিলেশনাল ডাটাবেস ম্যানেজমেন্ট সিস্টেম (RDBMS)। PostgreSQL এর মাধ্যমে খুব সহজেই সুসংগঠিত ভাবে তথ্য সংরক্ষণ, পরিচালনা এবং পুনরুদ্ধারের কাজে ব্যবহার করা যায়। মর্ডান ওয়েব অ্যাপ্লিকেশন, ডেটা ওয়্যারহাউসিং এবং অ্যানালিটিক্সে PostgreSQL অত্যন্ত নির্ভরযোগ্য একটি মাধ্যম।

### কেন PostgreSQL ব্যবহার করা হয়:

- PostgreSQL সম্পুর্ন ওপেন-সোর্স এবং ফ্রি, যার ফলে যে কোনো ধরনের প্রজেক্টে লাইসেন্সের কোনো সমস্যা তৈরী হয় না।

- SQL ও উন্নত ডেটা টাইপ (যেমন JSON, array) সাপোর্ট করে

- ACID-compliant, তাই লেনদেন নির্ভরযোগ্য হয়

- এক্সটেনসিবল - নিজস্ব ফাংশন ও ডেটা টাইপ তৈরি করা যায়

- বড় অ্যাপ্লিকেশনের জন্য সহজে স্কেল করা যায়

### Code Example:

```sql
-- Create a table
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  email TEXT UNIQUE NOT NULL
);

-- Insert data
INSERT INTO users (name, email) VALUES ('fahim', 'fahim@example.com');

-- Query data
SELECT * FROM users;

```

## What is the difference between the VARCHAR and CHAR data types?

PostgreSQL-এ VARCHAR এবং CHAR উভয়ই টেক্সট (যেমন নাম বা শব্দ) সংরক্ষণের জন্য ব্যবহৃত হয়, কিন্তু এদের কাজের ধরন আলাদা:

CHAR(n) সবসময় ঠিক n সংখ্যক ক্যারেক্টার জায়গা নেয়। যদি আপনি ছোট কোনো শব্দ সংরক্ষণ করেন, তাহলে এটি বাকিটা ফাঁকা জায়গা (space) দিয়ে পূরণ করে।
অন্যদিকে, VARCHAR(n) যতটুকু প্রয়োজন ততটুকু জায়গা নেয়, অতিরিক্ত স্পেস যোগ করে না।

VARCHAR (Variable Character):
যেকোনো দৈর্ঘ্যের টেক্সট সংরক্ষণ করতে পারে, তবে একটি নির্দিষ্ট সীমা পর্যন্ত (যেমন, VARCHAR(50) 50টি অক্ষর পর্যন্ত সংরক্ষণ করতে পারে)।
শুধুমাত্র টেক্সটের জন্য প্রয়োজনীয় জায়গা ব্যবহার করে। উদাহরণস্বরূপ, VARCHAR(50)-তে "cat" সংরক্ষণ করলে মাত্র 3টি অক্ষরের জায়গা নেয়।
বিভিন্ন দৈর্ঘ্যের টেক্সটের জন্য উপযুক্ত, যেমন ব্যবহারকারীর নাম বা বিবরণ।
টেক্সটের দৈর্ঘ্য ট্র্যাক করতে হয়, তাই কিছুটা ধীর।
CHAR (Fixed Character):
নির্দিষ্ট দৈর্ঘ্যের টেক্সট সংরক্ষণ করে (যেমন, CHAR(5) সবসময় ঠিক 5টি অক্ষর সংরক্ষণ করে)।
টেক্সট ছোট হলে, বাকি জায়গা ফাঁকা স্পেস দিয়ে পূরণ করে। উদাহরণস্বরূপ, CHAR(5)-এ "cat" সংরক্ষণ করলে "cat " হবে (2টি ফাঁকা স্পেস যোগ হবে)।
টেক্সটের দৈর্ঘ্য যাই হোক, সবসময় একই পরিমাণ জায়গা ব্যবহার করে।
নির্দিষ্ট দৈর্ঘ্যের তথ্যের জন্য দ্রুত, যেমন কোড (যেমন, "USA" বা "NY")।

### Code Example:

```sql
CREATE TABLE example (
  fixed CHAR(5),
  variable VARCHAR(5)
);

INSERT INTO example (fixed, variable) VALUES ('Hi', 'Hi');

SELECT fixed, variable FROM example;

```

এই টেবিলে 'Hi' ইনসার্ট করার পরে:

- fixed কলামে থাকবে 'Hi ' (ফাঁকা স্পেসসহ)
- variable কলামে থাকবে 'Hi' (কোনো বাড়তি স্পেস ছাড়া)

## Explain the purpose of the WHERE clause in a SELECT statement.

SELECT স্টেটমেন্টে WHERE ক্লজ ব্যবহার করা হয় ডেটা ফিল্টার করার জন্য। এটি ডেটাবেসকে বলে যে, শুধুমাত্র সেইসব রো (row) প্রদান করো যেগুলো একটি নির্দিষ্ট শর্ত পূরণ করে।

### Code Example:

```sql
SELECT * FROM users
WHERE age > 18;
```

এর মানে হলো:
১৮ বছরের বেশি বয়স যাদের, তাদের ডেটা দেখাও।

যদি WHERE না থাকে, তাহলে সব রো দেখাবে।
WHERE থাকলে শুধু শর্ত অনুযায়ী মিল থাকা রো দেখাবে।

## What are the LIMIT and OFFSET clauses used for?

LIMIT এবং OFFSET ক্লজ ব্যবহার করা হয় ডেটাবেস থেকে কতটি রো(row) আনতে হবে এবং কোন রো(row) থেকে শুরু করতে হবে তা নিয়ন্ত্রণ করার জন্য।

- LIMIT বলে দেয়, কতটি রো(row) দেখাবে।

- OFFSET বলে দেয়, শুরুর আগে কতটি রো(row) স্কিপ (এড়িয়ে) করবে।

### Code Example

```sql
SELECT * FROM users
LIMIT 5 OFFSET 10;
```

এর মানে:
প্রথম ১০টি রো(row) স্কিপ করো, তারপর পরের ৫টি রো(row) দেখাও।

এটি সাধারণত pagination এর জন্য ব্যবহার হয় যেমন: একটি লিস্টে প্রতিটি পেজে ৫টি করে আইটেম থাকলে, পেজ ২-এ দেখাতে হলে প্রথম ৫টি OFFSET 5 দিয়ে স্কিপ করে, পরের ৫টি LIMIT 5 দিয়ে দেখানো হয়।

## Explain the Primary Key and Foreign Key concepts in PostgreSQL.

### Primary Key:

Primary Key এমন একটি কলাম (বা কলামগুলোর সমষ্টি), যা একটি টেবিলের প্রতিটি রো (row) কে অন্যদের থেকে আলাদা করে চিহ্নিত করে।

- এটি NULL হতে পারে না

- এর মান অবশ্যই ইউনিক (অনন্য) হতে হবে

### Code Example

```sql
CREATE TABLE students (
  student_id SERIAL PRIMARY KEY,
  name TEXT
);
```

এখানে student_id হলো Primary Key: প্রত্যেক শিক্ষার্থীর জন্য এটি একটি বিশেষ ও আলাদা আইডি।

### Foreign Key:

Foreign Key এমন একটি কলাম যা অন্য টেবিলের Primary Key এর সাথে সংযোগ তৈরি করে।

- এটি নিশ্চিত করে যে, ডেটার মধ্যে বৈধ সম্পর্ক আছে

### Code Example

```sql

CREATE TABLE enrollments (
  enrollment_id SERIAL PRIMARY KEY,
  student_id INT REFERENCES students(student_id),
  course TEXT
);
```

এখানে student_id হলো Foreign Key, যা students টেবিলের student_id এর সাথে সংযুক্ত।
এটি নিশ্চিত করে যে শুধুমাত্র বৈধ ছাত্র আইডি ব্যবহার করে এনরোলমেন্ট করা যাবে।
