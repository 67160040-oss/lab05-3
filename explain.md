# Challenge: Create a Person Object

```text
console.log("\n=== Challenge: Person Object ===");
const student = {
  firstName: "Alice",
  lastName: "Smith",
  age: 20,
  gpa: 3.8,
  courses: ["HTML", "CSS", "JavaScript"],
  isActive: true,
  // Method (function in object)
  getFullName: function () {
    return `${this.firstName} ${this.lastName}`;
  },
  getInfo: function () {
    return `${this.getFullName()}, Age: ${this.age}, GPA: ${this.gpa}`;
  },
};
console.log("Student object:");
console.log(student);
console.log("Full name:", student.getFullName());
console.log("Info:", student.getInfo());
console.log("Courses:", student.courses.join(", "));
```

- บรรทัดเเรกเเสดงหัวข้อที่ชื่อ Create a Person Object

- สร้าง Object student เก็บข้อมูลของนักเรียนไว้ใน object

- ประกอบด้วย ข้อมูล (properties) และ ฟังก์ชัน (methods)

- แสดงข้อความและ object ทั้งหมด
- console.log("Student object:"); บรรทัดแรกแสดงข้อความธรรมดา
- console.log(student); บรรทัดที่สองแสดงข้อมูลทั้งหมดใน object

- เรียกใช้ method getFullName()
- เรียกใช้ this.getFullName() และอ่านค่า age เเละ gpa
- แสดงรายวิชาที่เรียน

```text
{
    console.log("Courses:", student.courses.join(", "));
}
```

## ผลลัพธ์ที่แสดง

```text
=== Challenge: Person Object ===
Student object:
{
  firstName: "Alice",
  lastName: "Smith",
  age: 20,
  gpa: 3.8,
  courses: ["HTML", "CSS", "JavaScript"],
  isActive: true,
  getFullName: ƒ (),
  getInfo: ƒ ()
}
Full name: Alice Smith
Info: Alice Smith, Age: 20, GPA: 3.8
Courses: HTML, CSS, JavaScript
```

---

# Returning Objects

```text
function createUser(firstName, lastName, age) {
  return {
    firstName, // shorthand for firstName: firstName -- สําคัญมาก
    lastName,
    age,
    email: `${firstName.toLowerCase()}.${lastName.toLowerCase()}@example.com`,
    getFullName() {
      // shorthand for getFullName: function() {}
      return `${this.firstName} ${this.lastName}`;
    },
    getAge() {
      return this.age;
    },
  };
}
console.log("\nReturning Objects:");
const newUser = createUser("John", "Doe", 30);
console.log(newUser);
console.log("Email:", newUser.email);
console.log("Full name:", newUser.getFullName());
```

- การประกาศฟังก์ชัน createUser รับค่า 3 ค่า firstName lastName age
- การสร้าง email อัตโนมัติ (email: `${firstName.toLowerCase()}.${lastName.toLowerCase()}@example.com`,)

```text
getFullName() {
 return `${this.firstName} ${this.lastName}`;
}
```

- ใช้ this เพื่ออ้างถึง object ที่ถูกสร้างขึ้น
- ดึง firstName และ lastName มารวมกัน

```text
getAge() {
  return this.age;
}
```

- Method getAge() คืนค่าอายุของผู้ใช้จาก object
- การเรียกใช้ฟังก์ชัน createUser (const newUser = createUser("John", "Doe", 30); )
- แสดงข้อมูลทั้งหมดของ object newUser (console.log(newUser); )
- เข้าถึง property email ของ object (console.log("Email:", newUser.email); )
- เรียก method getFullName() (console.log("Full name:", newUser.getFullName()); )

## ผลลัพธ์ที่แสดง

```text
Returning Objects:
{
  firstName: "John",
  lastName: "Doe",
  age: 30,
  email: "john.doe@example.com",
  getFullName: ƒ (),
  getAge: ƒ ()
}
Email: john.doe@example.com
Full name: John Doe
```

---

# Function as Parameter (Callback)

```text
function processArray(arr, callback) {
  const result = [];
  for (const item of arr) {
    result.push(callback(item));
  }
  return result;
}
const numbers = [1, 2, 3, 4, 5];
const doubled = processArray(numbers, (x) => x * 2);
const squared = processArray(numbers, (x) => x * x);
console.log("\nCallback Function:");
console.log("Original:", numbers);
console.log("Doubled:", doubled);
console.log("Squared:", squared);
```

- processArray รับ array และ callback function
- วนลูปแต่ละค่าใน array แล้วเอาไปประมวลผลด้วย callback
- doubled ใช้ callback คูณ 2
- squared ใช้ callback ยกกำลังสอง
- ได้ array ใหม่ตามเงื่อนไขที่ส่งเข้าไป

## ผลลัพธ์ที่แสดง

```text
Callback Function:
Original: [1, 2, 3, 4, 5]
Doubled: [2, 4, 6, 8, 10]
Squared: [1, 4, 9, 16, 25]

```

---

# Short-Circuit Evaluation

```text
console.log("\nShort-Circuit Evaluation:");
const user = { name: "John", age: 25 };
const admin = null;
// OR: use default value
const userName = admin?.name || user.name || "Anonymous";
console.log("User name:", userName);
// ?. คือการใช ้Optional Chaining - เป็นวิธีที่ปลอดภัยในการเข ้าถึง properties ของ object ที่อาจเป็น null หรือ undefined
// admin?.name ก็คือ ถ ้า admin มีค่า ให้เข ้าถึง .name ไม่เชนนั้นให ้คืนค่า ่ undefined
// 1. admin?.name
// - admin คือ null ❌
// - ไม่ error, สงคืน ่ undefined
// 2. undefined || user.name
// - user.name คือ "John" ✅
// - ใชค่านี้ → " ้ John"
// 3. ผลลัพธ์: "John"
// AND: check before accessing
const userProfile = user && user.profile;
console.log("User profile:", userProfile); // undefined
```

- admin?.name → admin เป็น null ⇒ ได้ undefined (ไม่ error)
- undefined || user.name → ได้ "John"
- เลยแสดง User name: John
- user && user.profile → user มีค่า แต่ profile ไม่มี ⇒ undefined

## ผลลัพธ์ที่แสดง

```text
Short-Circuit Evaluation:
User name: John
User profile: undefined
```

---

# Form Validation

```text
function validateRegistration(formData) {
  // Create validation result object
  const errors = [];
  // Validate name
  if (!formData.name || formData.name.trim() === "") {
    errors.push("Name is required");
  } else if (formData.name.length < 3) {
    errors.push("Name must be at least 3 characters");
  }
  // Validate email
  if (!formData.email || formData.email.indexOf("@") === -1) {
    errors.push("Valid email is required");
  }
  // Validate age
  if (!formData.age || formData.age < 18) {
    errors.push("Must be 18 or older");
  }
  // Validate password
  if (!formData.password || formData.password.length < 6) {
    errors.push("Password must be at least 6 characters");
  }
  // Check if agree to terms
  if (!formData.agreeToTerms) {
    errors.push("Must agree to terms");
  }
  return {
    isValid: errors.length === 0,
    errors: errors,
  };
}
console.log("\nForm Validation:");
const validUser = {
  name: "John Doe",
  email: "john@example.com",
  age: 25,
  password: "securepass123",
  agreeToTerms: true,
};
const invalidUser = {
  name: "Jo",
  email: "invalidemail",
  age: 15,
  password: "pass",
  agreeToTerms: false,
};
console.log("Valid user:", validateRegistration(validUser));
console.log("Invalid user:", validateRegistration(invalidUser));
```

- ฟังก์ชัน validateRegistration ทำหน้าที่ ตรวจสอบความถูกต้องของข้อมูลสมัครสมาชิก โดยรับข้อมูลผู้ใช้เข้ามาในรูปแบบ object (formData)
- เริ่มต้นด้วยการสร้าง array ชื่อ errors ใช้เก็บข้อความแจ้งข้อผิดพลาด หากข้อมูลไม่ผ่านเงื่อนไข
- ตรวจสอบชื่อ (name)
- ถ้าไม่มีชื่อหรือเป็นค่าว่าง → เพิ่ม error
- ถ้าชื่อสั้นกว่า 3 ตัวอักษร → เพิ่ม error
- ตรวจสอบอีเมล (email)
- ถ้าไม่มี @ หรือไม่มีค่า → ถือว่าอีเมลไม่ถูกต้อง
- ตรวจสอบอายุ (age)
- ถ้าอายุน้อยกว่า 18 ปี → ไม่ผ่านเงื่อนไข
- ตรวจสอบรหัสผ่าน (password)
- ต้องมีอย่างน้อย 6 ตัวอักษร
- ตรวจสอบการยอมรับเงื่อนไข (agreeToTerms)
- ถ้าไม่ได้ติ๊กยอมรับ → เพิ่ม error
- เมื่อเช็คครบทุกเงื่อนไข
- ถ้า errors ว่าง → isValid เป็น true
- ถ้ามี error อย่างน้อย 1 ข้อ → isValid เป็น false
- ฟังก์ชันส่งผลลัพธ์กลับเป็น object ที่บอกว่า
- ข้อมูลถูกต้องหรือไม่ (isValid)
- มีข้อผิดพลาดอะไรบ้าง (errors)

## ผลลัพธ์ที่แสดง

```text
Form Validation:
Valid user: { isValid: true, errors: [] }
Invalid user: {
  isValid: false,
  errors: [
    "Name must be at least 3 characters",
    "Valid email is required",
    "Must be 18 or older",
    "Password must be at least 6 characters",
    "Must agree to terms"
  ]
}
```

---

# Chaining methods

```text
console.log("\nMethod chaining:");
const data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
// Filter even > map to string > join
const evenStrings = data
  .filter((n) => n % 2 === 0) // [2, 4, 6, 8, 10]
  .map((n) => `${n}²=${n * n}`) // ["2²=4", "4²=16", ...]
  .join(", "); // "2²=4, 4²=16, ..."
console.log("Even numbers squared:", evenStrings);
// Calculate average with reduce and length
const numbers2 = [10, 20, 30, 40, 50];
const average = numbers2.reduce((sum, n) => sum + n, 0) / numbers2.length;
console.log("Average:", average);
```

- Method Chaining / filter คัดเฉพาะเลขคู่จาก array / map แปลงเลขคู่ให้เป็นข้อความพร้อมยกกำลังสอง / join รวม array เป็น string เดียว
- การหาค่าเฉลี่ย / reduce รวมค่าทั้งหมดใน array / นำผลรวมไปหารด้วยจำนวนสมาชิก (length)

## ผลลัพธ์ที่แสดง

```text
Method chaining:
Even numbers squared: 2²=4, 4²=16, 6²=36, 8²=64, 10²=100
Average: 30

```

---

# Challenge: Student Grades

```text
const students = [
  { name: "Alice", score: 95 },
  { name: "Bob", score: 75 },
  { name: "Charlie", score: 85 },
  { name: "Diana", score: 92 },
  { name: "Eve", score: 88 },
];
console.log("\nChallenge: Student Analysis");
console.log("Students:", students);
// 1. Get all names
const names = students.map((s) => s.name);
console.log("Names:", names.join(", "));
// 2. Filter high scorers (>= 85)
const highScorers = students.filter((s) => s.score >= 85);
console.log(
  "High scorers:",
  highScorers.map((s) => `${s.name} (${s.score})`).join(", ")
);
// 3. Calculate class average
const classAverage =
  students.reduce((sum, s) => sum + s.score, 0) / students.length;
console.log("Class average:", classAverage.toFixed(2));
// 4. Find top scorer
const topScorer = students.reduce((top, s) => (s.score > top.score ? s : top));
console.log("Top scorer:", `${topScorer.name} (${topScorer.score})`);
// 5. Create summary
const summary = students
  .map((s) => ({
    ...s,
    grade: s.score >= 90 ? "A" : s.score >= 80 ? "B" : "C",
  }))
  .sort((a, b) => b.score - a.score);
console.log("Summary (sorted):");
summary.forEach((s) => console.log(` ${s.name}: ${s.score} (${s.grade})`));
console.log("\n✅ Activity 4 completed!");
```

- ใช้ map ดึงชื่อของนักเรียนทั้งหมดออกมา
- ใช้ filter คัดนักเรียนที่ได้คะแนนตั้งแต่ 85 ขึ้นไป
- ใช้ reduce รวมคะแนนทั้งหมดแล้วหารเพื่อหาค่าเฉลี่ย
- ใช้ reduce หาเด็กที่ได้คะแนนสูงสุด
- ใช้ map เพิ่มเกรด (A, B, C) และ sort เรียงคะแนนจากมากไปน้อย

## ผลลัพธ์ที่แสดง

```text
Challenge: Student Analysis
Students: [
  { name: "Alice", score: 95 },
  { name: "Bob", score: 75 },
  { name: "Charlie", score: 85 },
  { name: "Diana", score: 92 },
  { name: "Eve", score: 88 }
]
Names: Alice, Bob, Charlie, Diana, Eve
High scorers: Alice (95), Charlie (85), Diana (92), Eve (88)
Class average: 87.00
Top scorer: Alice (95)
Summary (sorted):
 Alice: 95 (A)
 Diana: 92 (A)
 Eve: 88 (B)
 Charlie: 85 (B)
 Bob: 75 (C)

✅ Activity 4 completed!

```

---

## Activity 5: Integration - Quiz Application

```text
// ============================================
// Activity 5: Integration - Quiz Application
// ============================================
console.log("🎯🎯 === QUIZ APPLICATION === 🎯🎯\n");
// Quiz data
const quizzes = [
  {
    question: "What is 5 + 3?",
    options: ["8", "7", "6", "9"],
    correctAnswer: 0, // Index of correct option
  },
  {
    question: "What is the capital of Thailand?",
    options: ["Phuket", "Bangkok", "Chiang Mai", "Pattaya"],
    correctAnswer: 1,
  },
  {
    question: "What is the largest planet?",
    options: ["Mars", "Saturn", "Jupiter", "Neptune"],
    correctAnswer: 2,
  },
  {
    question: "What is 2^8?",
    options: ["128", "256", "64", "512"],
    correctAnswer: 1,
  },
  {
    question: "Which is NOT a JavaScript data type?",
    options: ["string", "class", "symbol", "boolean"],
    correctAnswer: 1,
  },
];
// Quiz results
let results = [];
// Process each quiz
quizzes.forEach((quiz, index) => {
  const userAnswer = Math.floor(Math.random() * 4); // จําลองการทํา quiz
  const isCorrect = userAnswer === quiz.correctAnswer;
  results.push({
    questionNum: index + 1,
    question: quiz.question,
    userAnswer: quiz.options[userAnswer],
    correctAnswer: quiz.options[quiz.correctAnswer],
    isCorrect: isCorrect,
  });
});
// Display results
console.log("QUIZ RESULTS:");
console.log("─".repeat(60));
results.forEach((result) => {
  const status = result.isCorrect ? "✅ CORRECT" : "❌ WRONG";
  console.log(`Q${result.questionNum}: ${result.question}`);
  console.log(` Your answer: ${result.userAnswer}`);
  if (!result.isCorrect) {
    console.log(` Correct answer: ${result.correctAnswer}`);
  }
  console.log(` ${status}`);
  console.log();
});
// Calculate score
const correctCount = results.filter((r) => r.isCorrect).length;
const score = (correctCount / results.length) * 100;
console.log("─".repeat(60));
console.log(
  `FINAL SCORE: ${correctCount}/${results.length} (${score.toFixed(1)}%)`
);
// Grade assignment
let grade;
if (score >= 90) {
  grade = "A";
} else if (score >= 80) {
  grade = "B";
} else if (score >= 70) {
  grade = "C";
} else if (score >= 60) {
  grade = "D";
} else {
  grade = "F";
}
console.log(`GRADE: ${grade}`);
// Feedback
console.log("\nFEEDBACK:");
if (score === 100) {
  console.log("🌟🌟 Perfect score! Excellent work!");
} else if (score >= 80) {
  console.log("👍👍 Great job! Keep practicing.");
} else if (score >= 60) {
  console.log("📚📚 Good effort. Review the material and try again.");
} else {
  console.log("💪💪 Keep practicing. You'll improve!");
}
// Statistics
console.log("\n📊📊 STATISTICS:");
console.log(`Total questions: ${results.length}`);
console.log(`Correct: ${correctCount}`);
console.log(`Incorrect: ${results.length - correctCount}`);
console.log(`Success rate: ${score.toFixed(1)}%`);
// Category breakdown (if applicable)
const byCorrectness = results.reduce(
  (acc, r) => {
    acc[r.isCorrect ? "correct" : "incorrect"]++;
    return acc;
  },
  { correct: 0, incorrect: 0 }
);
console.log("\nAnswer breakdown:");
console.log(` ✅ Correct: ${byCorrectness.correct}`);
console.log(` ❌ Incorrect: ${byCorrectness.incorrect}`);
console.log("\n✅ All activities completed!");
console.log("━".repeat(60));
```

- สร้าง quiz data

  - แต่ละคำถามเก็บ question, options, correctAnswer

- จำลองการทำ quiz

  - Math.random() เลือกคำตอบผู้ใช้แบบสุ่ม
  - เก็บผลลัพธ์ใน array results

- แสดงผลลัพธ์ทีละคำถาม

  - ถ้าคำตอบถูก → ✅ CORRECT
  - ถ้าไม่ถูก → ❌ WRONG + แสดงคำตอบที่ถูกต้อง

- คำนวณคะแนนรวม

  - นับจำนวนถูก → correctCount
  - แปลงเป็นเปอร์เซ็นต์ → score

- กำหนดเกรด

  - 90+ → A, 80+ → B, 70+ → C, 60+ → D, ต่ำกว่า → F

- แสดง feedback

  - ขึ้นกับคะแนน

- สรุปสถิติ
  - จำนวนคำถาม, ถูก, ผิด, อัตราความสำเร็จ
  - แยกจำนวนถูก/ผิดแบบง่าย ๆ (byCorrectness)

## ผลลัพธ์ที่แสดง

```text
🎯🎯 === QUIZ APPLICATION === 🎯🎯

QUIZ RESULTS:
────────────────────────────────────────────
Q1: What is 5 + 3?
 Your answer: 8
 ✅ CORRECT

Q2: What is the capital of Thailand?
 Your answer: Chiang Mai
 Correct answer: Bangkok
 ❌ WRONG

Q3: What is the largest planet?
 Your answer: Jupiter
 ✅ CORRECT

Q4: What is 2^8?
 Your answer: 256
 ✅ CORRECT

Q5: Which is NOT a JavaScript data type?
 Your answer: class
 ✅ CORRECT

────────────────────────────────────────────
FINAL SCORE: 4/5 (80.0%)
GRADE: B

FEEDBACK:
👍👍 Great job! Keep practicing.

📊📊 STATISTICS:
Total questions: 5
Correct: 4
Incorrect: 1
Success rate: 80.0%

Answer breakdown:
 ✅ Correct: 4
 ❌ Incorrect: 1

✅ All activities completed!

```
