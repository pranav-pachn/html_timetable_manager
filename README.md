# HTML Timetable Manager

A purely client-side browser application for Principals and Administrators to design, generate, and manage school timetables seamlessly.

## Workflow for the Principal

The application stores all imported setup data securely in your browser's `localStorage`. To generate a timetable from scratch, follow these exact steps:

### 1. Setup the Foundation (Master Data)
Go to the **Setup** section to define the core structural data of the school:
*   **Bulk Classes & Sections:** Import your `class-sections.csv` to establish the grades and sections in your school (e.g., Grade-I-A, Grade-I-B). You can also type them in manually.
*   **Bulk Subjects:** Import your `subjects-code.csv` to establish all available subjects.
*   **Teacher List:** Import your `teacher-list.csv` to register all faculty members with their basic contact details and class teacher assignments.

### 2. Configure the Timetable Parameters
In the **Timetable Configuration** panel, set your scheduling constraints:
*   **School Days:** Set the operating days (e.g., Monday,Tuesday,Wednesday,Thursday,Friday,Saturday).
*   **Periods per Day:** Set how many periods are in a standard day.
*   **Max Periods Per Teacher:** Determine the maximum workload any individual teacher can be assigned per week.

### 3. Import Teacher-Subject Mappings
Upload your `teacher-mapping.csv` in the **Teacher Grade-Section Subject Mapping** panel. This is the most crucial step. It tells the system:
*   Which Teacher teaches which Subject to which Grade-Section.
*   **Periods Per Week:** How many periods this mapping requires.
*   **Fixed Periods:** Specific locked periods (e.g., `1` for P1, `5,6` for P5 and P6).
*   **Mode:** Whether the class is Individual (`0`) or Combined (`1`) (where multiple classes share the same teacher simultaneously).

### 4. Save and Generate
*   Once all data is imported and looks correct in the UI tables, click **Save Changes** at the top.
*   Click **Generate Timetable**. The built-in scheduling engine will automatically construct a complete, conflict-free timetable honoring your mappings, fixed periods, lab blocks, and combined classes.

### 5. Review and Refine
Navigate to the **View** section to visually inspect the results:
*   **Teacher View:** Ensure no teacher is double-booked and verify their workloads.
*   **Class View:** Ensure all periods are filled correctly.
*   **Subject View:** Track subject distributions.

*(Optional Alternative)*: If you prefer to generate the timetable externally, you can use the **AI Prompt** tab to copy a prompt to feed into an LLM (like ChatGPT or Claude), and then use **Upload Timetable** to import the generated CSV.

---

## Required CSV Formats

### 1. Class Sections CSV
```csv
Class,Section,Teaching Mode,Combined Group
Grade-I,A,,
Grade-I,B,,
```

### 2. Subjects CSV
```csv
Subject Code,Subject Name
MTH,Maths
ENG,English
SCI,Science
```

### 3. Teacher List CSV
```csv
Teacher ID,Teacher Name,Class Teacher Subject,Class Teacher Grade,Class Teacher Section,Phone,Email
T001,Indira,MTH,Grade-I,A,9876543210,indira@school.com
T002,Sai Priya,EVS,Grade-I,B,,
```

### 4. Teacher Grade-Section Subject Mapping CSV
```csv
Teacher ID,Grade-Section,Subject,Periods Per Week,Fixed Periods,Mode
T001,Grade-I-A,MTH,5,,0
T002,Grade-I-A,EVS,4,1,0
T003,Grade-V-A;Grade-V-B,PT,2,,1
```

---

## Output CSV Format
If you choose to upload a manually generated timetable or one from an AI, ensure it follows this strict CSV format:

```csv
Class-Section,Day,P1,P2,P3,P4,P5,P6,P7,P8
Grade-I-A,Monday,T001:Indira:MTH,T002:Sai:EVS,,,,,,,
```

### Cell Separator Rules (Important)
*   Use this structure strictly: `TeacherID:TeacherName:Subject`
*   `:` separates TeacherID and TeacherName
*   `:` separates TeacherName and Subject
*   `-` separates Class and Section (e.g., `Grade-I-A`)

## Excel Upload Formats
Supported Excel formats for uploading existing timetables:
*   `Standard (Sheet-per-Class)`: One sheet per class, row-wise day timetable.
*   `STATE TIME TABLE (19.07.2025)`: Teacher-wise matrix with day blocks and period numbers.

Before uploading an Excel file, choose the matching format from the Excel Format dropdown in the Upload section.
