# BrightSpace D2L Organization Plugin

PowerQuery Plugin for exporting the following information from PowerSchool &rarr; BrightSpace. This plugin creates the following exports:

- [BrightSpace D2L Organization Plugin](#brightspace-d2l-organization-plugin)
  - [Notes](#notes)
    - [SCH Plugins](#sch-plugins)
  - [1 Other](#1-other)
    - [Fields Provided \& Used](#fields-provided--used)
    - [Data Export Manager Setup](#data-export-manager-setup)
    - [Query Setup for `named_queries.xml`](#query-setup-for-named_queriesxml)
  - [1 Other - Parent Schools](#1-other---parent-schools)
    - [Fields Provided \& Used](#fields-provided--used-1)
    - [Data Export Manager Setup](#data-export-manager-setup-1)
    - [Query Setup for `named_queries.xml`](#query-setup-for-named_queriesxml-1)
  - [2 Departments](#2-departments)
    - [Fields Provided \& Used](#fields-provided--used-2)
    - [Data Export Manager Setup](#data-export-manager-setup-2)
    - [Query Setup for `named_queries.xml`](#query-setup-for-named_queriesxml-2)
  - [3 Semesters](#3-semesters)
    - [Fields Provided \& Used](#fields-provided--used-3)
    - [Data Export Manager Setup](#data-export-manager-setup-3)
    - [Query Setup for `named_queries.xml`](#query-setup-for-named_queriesxml-3)
  - [4 Templates](#4-templates)
    - [Fields Provided \& Used](#fields-provided--used-4)
    - [Data Export Manager Setup](#data-export-manager-setup-4)
    - [Query Setup for `named_queries.xml`](#query-setup-for-named_queriesxml-4)
  - [5 Offerings](#5-offerings)
    - [Fields Provided \& Used](#fields-provided--used-5)
    - [Data Export Manager Setup](#data-export-manager-setup-5)
    - [Query Setup for `named_queries.xml`](#query-setup-for-named_queriesxml-5)
  - [5 Athletic Offerings](#5-athletic-offerings)
    - [Fields Provided \& Used](#fields-provided--used-6)
    - [Data Export Manager Setup](#data-export-manager-setup-6)
    - [Query Setup for `named_queries.xml`](#query-setup-for-named_queriesxml-6)
  - [6 Sections](#6-sections)
    - [Fields Provided \& Used](#fields-provided--used-7)
    - [Data Export Manager Setup](#data-export-manager-setup-7)
    - [Query Setup for `named_queries.xml`](#query-setup-for-named_queriesxml-7)
  - [6 Delete Sections UNUSED](#6-delete-sections-unused)
    - [Fields Provided \& Used](#fields-provided--used-8)
    - [Data Export Manager Setup](#data-export-manager-setup-8)
    - [Query Setup for `named_queries.xml`](#query-setup-for-named_queriesxml-8)

## Notes

### SCH Plugins

`SCH-` versions of named queries pull the same data from PowerSchool, but use the `schedule` versions of the tables. The `schedule` tables contain the non-committed version of the schedule for the following school year. This is typically done by creating an alias from `SCHEDULECC` to `CC` and `SCHEDULETERMS` to `TERMS` unless otherwise noted.

The CSV files produced by the `SCH-` versions should **not ever** be used on the production version of Brightspace. They create departments, semesters, templates and offerings with TEST in the name. These can, however, be safely run on the production side of PowerSchool.

## 1 Other

Create school level org units. Creates/updates schools: 0: District Office, 1: UE, 10: ECC, 2: MS, 2: HS, 5: Transfered Out, 999999: Graduated

### Fields Provided & Used

**PROVIDES FIELDS**

- `code` used in [2-Department](#2-departments) as `custom_code` 

|Field |Format |example |
|:-|:-|:-|
|`code`| _`SCHOOLS.SCHOOL_NUMBER`_| 1

### Data Export Manager Setup

- **Category:** Show All
- **Export From:** `NQ com.txoof.brightspace.org.01other`
 
**Labels Used on Export**

| Label |
|-|
|type|
|action|
|code|
|name|
|start_date|
|end_date|
|is_active|
|department_code|
|template_code|
|semester_code|
|offering_code|
|custom_code|

**Export Summary and Output Options**

- *Export File Name:* `1-Other-%d.csv`
- *Line Delimiter:* `LF`
- *Field Delimiter:* `,`
- *Character Set:* `UTF-8`
- *Include Column Headers:* `True`
- *Surround "field values" in Quotes:* TBD

### Query Setup for `named_queries.xml`

| header | table.field | value | NOTE |
|-|-|-|-|
|type| SCHOOLS.ID | _School_ | N1
|action| SCHOOLS.ID | _UPDATE_ | N1
|code| SCHOOLS.SCHOOL_NUMBER | _2_ |
|name| COURSES.SCHED_DEPARTMENT | _ASH Middle School_ |
|start_date| SCHOOLS.ID | '' | N1
|end_date| SCHOOLS.ID | '' | N1
|is_active| SCHOOLS.ID | '' | N1
|department_code| SCHOOLS.ID | '' | N1
|template_code| SCHOOLS.ID | '' | N1
|semester_code| SCHOOLS.ID | '' | N1
|offering_code| SCHOOLS.ID | '' | N1
|custom_code| SCHOOLS.ID | '' | N1

**NOTES**

**N1:** Field does not appear in database; use a known field such as `<column column=STUDENT.ID>header<\column>` to prevent an "unknown column error"

**Tables Used**

| Table |
|-|
|SCHOOLS|


## 1 Other - Parent Schools

Creates parent schools. Parent schools are special purpose schools that are used for enrolling parents as `Learners`. Parents enrolled with type `Guardian` are not visible to Intelligent Agent tools and do not appear in rosters. To make parents visible to IA tools, they need to appear as `Learners`.
### Fields Provided & Used

**PROVIDES FIELDS**

- `code` used in [2-Department](#2-departments) as `custom_code` 

|Field |Format |example |
|:-|:-|:-|
|`code`| _P\_`SCHOOLS.SCHOOL_NUMBER`_| P_1

### Data Export Manager Setup

- **Category:** Show All
- **Export From:** `NQ com.txoof.brightspace.org.01other_parents`
 
**Labels Used on Export**

| Label |
|-|
|type|
|action|
|code|
|name|
|start_date|
|end_date|
|is_active|
|department_code|
|template_code|
|semester_code|
|offering_code|
|custom_code|

**Export Summary and Output Options**

- *Export File Name:* `1-Other_Parent_School-%d.csv`
- *Line Delimiter:* `LF`
- *Field Delimiter:* `,`
- *Character Set:* `UTF-8`
- *Include Column Headers:* `True`
- *Surround "field values" in Quotes:* TBD

### Query Setup for `named_queries.xml`

| header | table.field | value | NOTE |
|-|-|-|-|
|type| SCHOOLS.ID | _School_ | N1
|action| SCHOOLS.ID | _UPDATE_ | N1
|code| 'P_'||SCHOOLS.SCHOOL_NUMBER | _P\_2_ |
|name| COURSES.SCHED_DEPARTMENT | _ASH Middle School - Parents_ |
|start_date| SCHOOLS.ID | '' | N1
|end_date| SCHOOLS.ID | '' | N1
|is_active| SCHOOLS.ID | '' | N1
|department_code| SCHOOLS.ID | '' | N1
|template_code| SCHOOLS.ID | '' | N1
|semester_code| SCHOOLS.ID | '' | N1
|offering_code| SCHOOLS.ID | '' | N1
|custom_code| SCHOOLS.ID | '' | N1

**NOTES**

**N1:** Field does not appear in database; use a known field such as `<column column=STUDENT.ID>header<\column>` to prevent an "unknown column error"

**Tables Used**

| Table |
|-|
|SCHOOLS|


## 2 Departments

### Fields Provided & Used

**PROVIDES FIELDS**

- `code` used in [4-Template](#4-templates) as `department_code` 

|Field |Format |example |
|:-|:-|:-|
|`code`| _`CC.SCHOOLID`_`_`_`COURSES.SCHED_DEPARTMENT`_| 2_MSEAL

### Data Export Manager Setup

- **Category:** Show All
- **Export From:** `NQ com.txoof.brightspace.org.02departments`

**Labels Used on Export**

| Label |
|-|
|type|
|action|
|code|
|name|
|start_date|
|end_date|
|is_active|
|department_code|
|template_code|
|semester_code|
|offering_code|
|custom_code|

**Export Summary and Output Options**

- *Export File Name:* `2-Departments-%d.csv`
- *Line Delimiter:* `LF`
- *Field Delimiter:* `,`
- *Character Set:* `UTF-8`
- *Include Column Headers:* `True`
- *Surround "field values" in Quotes:* TBD

### Query Setup for `named_queries.xml`

| header | table.field | value | NOTE |
|-|-|-|-|
|type| CC.ID | _department_ | N1
|action| CC.ID |_UPDATE_ | N1
|code| COURSES.SCHED_DEPARTMENT | _3\_HSPerArts_ |
|name| COURSES.SCHED_DEPARTMENT | _HSPerArts_ |
|start_date| CC.ID | '' | N1
|end_date| CC.ID | '' | N1
|is_active| CC.ID | '' | N1
|department_code| CC.ID | '' | N1
|template_code| CC.ID | '' | N1
|semester_code| CC.ID | '' | N1
|offering_code| CC.ID | '' | N1
|custom_code| SCHOOLS.SCHOOL_NUMBER | _1_ | 

**NOTES**

**N1:** Field does not appear in database; use a known field such as `<column column=STUDENT.ID>header<\column>` to prevent an "unknown column error"

**Tables Used**

| Table |
|-|
|STUDENTS|
|CC|
|COURSES|


## 3 Semesters

### Fields Provided & Used

**PROVIDES FIELDS**

`code` used in [5-Oferings](#5-offerings) as `semester_code`

|Field |Format |example |
|:-|:-|:-|
|`code`| `term_`_`cc.TermID`_| term_3102

### Data Export Manager Setup

- **Category:** Show All
- **Export From:**  `NQ com.txoof.brightpspace.org.03semesters`

**Labels Used on Export**

| Label |
|-|
|type|
|action|
|code|
|name|
|start_date|
|end_date|
|is_active|
|department_code|
|template_code|
|semester_code|
|offering_code|
|custom_code|

**Export Summary and Output Options**

- *Export File Name:* `3-Semesters-%d.csv`
- *Line Delimiter:* `LF`
- *Field Delimiter:* `,`
- *Character Set:* `UTF-8`
- *Include Column Headers:* `True`
- *Surround "field values" in Quotes:* TBD

### Query Setup for `named_queries.xml`

| header | table.field | value | NOTE |
|-|-|-|-|
|type| TERMS.ID | _semester_| N1|
|action| TERMS.ID | _update_ | N1|
|code| `'term_'\|\|TERMS.ID` | _term\_3100_ 
|name| TERMS.NAME | _2021-2022_ or _Semester 1_ or _Quarter 1_
|start_date| TERMS.ID | '' | N1
|end_date| TERMS.ID | '' | N1
|is_active| `TERMS.FIRSTDAY < sysdate < TERMS.LASTDAY` | _0_; _1_
|department_code| TERMS.ID | '' | N1
|template_code| TERMS.ID | '' | N1
|semester_code| TERMS.ID | '' | N1
|offering_code| TERMS.ID | '' | N1
|custom_code| TERMS.ID | '' | N1


**NOTES**

**N1:** Field does not appear in database; use a known field such as `<column column=STUDENT.ID>header<\column>` to prevent an "unknown column error"

**Tables Used**

| Table |
|-|
|TERMS|


## 4 Templates

### Fields Provided & Used

**PROVIDES FIELDS**

- `code` used in [5-Ofering](#5-offerings) as `template_code` 

|Field |Format |example |
|:-|:-|:-|
|`code`| `TEMPLATE_`_`CC.SCHOOLID`_`_`_`COURSES.SCHED_DEPARTMENT`_| TEMPLATE_2_MSEAL

**USES FIELDS:**

- `code` from [2-Deparments](#2-departments) as `department_code`

### Data Export Manager Setup

- **Category:** Show All
- **Export From:**  `NQ com.txoof.brightspace.org.04templates`

**Labels Used on Export**

| Label |
|-|
|type|
|action|
|code|
|name|
|start_date|
|end_date|
|is_active|
|department_code|
|template_code|
|semester_code|
|offering_code|
|custom_code|

**Export Summary and Output Options**

- *Export File Name:* `4-Templates-%d.csv`
- *Line Delimiter:* `LF`
- *Field Delimiter:* `,`
- *Character Set:* `UTF-8`
- *Include Column Headers:* `True`
- *Surround "field values" in Quotes:* TBD

### Query Setup for `named_queries.xml`
| header | table.field | value | NOTE |
|-|-|-|-|
|type| CC.ID | _course template_ | N1
|action| CC.ID |_UPDATE_ | N1
|code| COURSES.SCHED_DEPARTMENT | _Templ_3\_HSPerArts_ |
|name| COURSES.SCHED_DEPARTMENT | _HSPerArts_ |
|start_date| CC.ID | '' | N1
|end_date| CC.ID | '' | N1
|is_active| CC.ID | '' | N1
|department_code| COURSES.SCHED_DEPARTMENT | '' | N1
|template_code| CC.ID | '' | N1
|semester_code| CC.ID | '' | N1
|offering_code| CC.ID | '' | N1
|custom_code| CC.ID | '' | N1

**NOTES**

**N1:** Field does not appear in database; use a known field such as `<column column=STUDENT.ID>header<\column>` to prevent an "unknown column error"

**Tables Used**

| Table |
|-|
|STUDENTS|
|CC|
|COURSES|

## 5 Offerings

### Fields Provided & Used

**PROVIDES FIELDS**
`code` used in [6-Sections](#6-sections) as `offering_code` 

|Field |Format |example |
|:-|:-|:-|
|`code`| `co_`_`cc.SchoolID`_`_`_`cc.Course_Number`_| co_3_ITLDPROG1

**USES FIELDS:**

- `code` from [3-Semesters](#3-semesters) as `semester_code`
- `code` from [4-Templates](#4-templates) as `template_code`

### Data Export Manager Setup

- **Category:** Show All
- **Export From:**  `NQ com.txoof.brightspace.org.05offerings`

**Labels Used on Export**

| Label |
|-|
|type|
|action|
|code|
|name|
|start_date|
|end_date|
|is_active|
|department_code|
|template_code|
|semester_code|
|offering_code|
|custom_code|

**Export Summary and Output Options**

- *Export File Name:* `5-Offerings_500-%d.csv`
- *Line Delimiter:* `LF`
- *Field Delimiter:* `,`
- *Character Set:* `UTF-8`
- *Include Column Headers:* `True`
- *Surround "field values" in Quotes:* TBD

### Query Setup for `named_queries.xml`
| header | table.field | value | NOTE |
|-|-|-|-|
|type| CC.ID | _course offering_ | N1
|action| CC.ID | _UPDATE_ | N1
|code| _'co'\_schoolid\_coursenumber\_termid_ | _co\_3\_ITLDPROG1\_3100_
|name| C.COURSE_NAME | _IT Programming_ 
|start_date| CC.ID | '' | N1
|end_date| CC.ID | _term.lastday_ + 60 | N1
|is_active| CC.ID | _0_ | N1
|department_code| CC.ID | '' | N1
|template_code| CC.ID | '' | N1
|semester_code|   _'term'\_termid_ | _term\_3102_
|offering_code| CC.ID | '' | N1
|custom_code| CC.ID | '' | N1

**NOTES**

**N1:** Field does not appear in database; use a known field such as `<column column=STUDENT.ID>header<\column>` to prevent an "unknown column error"

**Tables Used**

| Table |
|-|
|STUDENTS|
|CC|
|TERMS|

## 5 Athletic Offerings

### Fields Provided & Used

**PROVIDES FIELDS**
`code` used in [6-Sections](#6-sections) as `offering_code` 

|Field |Format |example |
|:-|:-|:-|
|`code`| `co_athl_`_`Gen.Name`_| co_athl_Athletics - Baseball - MS

**USES FIELDS:**

- `code` from [3-Semesters](#3-semesters) as `semester_code`
- `code` from [4-Templates](#4-templates) as `template_code`

### Data Export Manager Setup

- **Category:** Show All
- **Export From:**  `NQ com.txoof.brightspace.org.05ath_offerings`

**Labels Used on Export**

| Label |
|-|
|type|
|action|
|code|
|name|
|start_date|
|end_date|
|is_active|
|department_code|
|template_code|
|semester_code|
|offering_code|
|custom_code|

**Export Summary and Output Options**

- *Export File Name:* `5-Offerings_501_Ath-%d.csv`
- *Line Delimiter:* `LF`
- *Field Delimiter:* `,`
- *Character Set:* `UTF-8`
- *Include Column Headers:* `True`
- *Surround "field values" in Quotes:* TBD

### Query Setup for `named_queries.xml`
| header | table.field | value | NOTE |
|-|-|-|-|
|type| GEN.ID | _course offering_ | N1
|action| GEN.ID | _UPDATE_ | N1
|code| GEN.name | _co\_ath\_Athletics - Baseball - MS_
|name| GEN.name | _Athletics - Baseball - MS_ 
|start_date| GEN.ID | '' | N1
|end_date| GEN.ID | '' | N1
|is_active| GEN.ID | _0_ | N1
|department_code| GEN.ID | '' | N1
|template_code| GEN.ID | '' | N1
|semester_code| GEN.ID | _term\_ATH_ | N1 
|offering_code| GEN.ID | '' | N1
|custom_code| GEN.ID | '' | N1

**NOTES**

**N1:** Field does not appear in database; use a known field such as `<column column=STUDENT.ID>header<\column>` to prevent an "unknown column error"

**Tables Used**

| Table |
|-|
|STUDENTS|
|GEN|


## 6 Sections

### Fields Provided & Used

**PROVIDES FIELDS:**

* `code` used in 08_Enrolments as `parent_code` 

|Field |Format |example |
|:-|:-|:-|
|`code`| `cs_`_`cc.schoolID`_`_`_`cc.course_number`_`_`_`cc.termid`_| 

**USES FIELDS:**

- `code` from [3-Semesters](#3-semesters) as `semester_code`
- `code` from [5-Offerings](#5-offerings) as `offering_code`

### Data Export Manager Setup

- **Category:** Show All
- **Export From:**  `NQ com.txoof.brightspace.org.06sections`

**Labels Used on Export**

| Label |
|-|
|type|
|action|
|code|
|name|
|start_date|
|end_date|
|is_active|
|department_code|
|template_code|
|semester_code|
|offering_code|
|custom_code|

**Export Summary and Output Options**

- *Export File Name:* `6-Sections-%d.csv`
- *Line Delimiter:* `LF`
- *Field Delimiter:* `,`
- *Character Set:* `UTF-8`
- *Include Column Headers:* `True`

### Query Setup for `named_queries.xml`
| header | table.field | value | NOTE |
|-|-|-|-|
|type| CC.ID | _course offering_ | N1
|action| CC.ID | _UPDATE_ | N1
|code| _'cs'\_schoolid\_coursenumber\_termid\_block\_sectionid_ | _cs\_3\_ITLDROB\_3101\_C\_12345_
|name| C.COURSE_NAME | _IT Robotics I - B Block (S2) Smith_
|start_date| CC.ID | '' | N1
|end_date| CC.ID | '' | N1
|is_active| CC.ID | '' | N1
|department_code| CC.ID | '' | N1
|template_code| CC.ID | '' | N1
|semester_code|   CC.ID | '' | N1
|offering_code| _'co'\_schoolid\_coursenumber\_termid_ | _co\_3\_ITLDROB\_3101_
|custom_code| CC.ID | '' | N1

**NOTES**

**N1:** Field does not appear in database; use a known field such as `<column column=STUDENT.ID>header<\column>` to prevent an "unknown column error"

**Tables Used**

| Table |
|-|
|STUDENTS|
|CC|
|TERMS|
|TEACHERS|
|SCHOOLSTAFF|
|COURSES|

## 6 Delete Sections UNUSED

Delete sections from previous school year. This query will clean out sections that are no longer in use. This pattern is useful when courses are reused over and over again and each year additional blocks are attached to the courses.

### Fields Provided & Used

**PROVIDES FIELDS:**

`code` used in ?? as `????` 

|Field |Format |example |
|:-|:-|:-|
|`code`| `cs_`_`cc.schoolID`_`_`_`cc.course_number`_`_`_`cc.termid`_| 

**USES FIELDS:**

- `code` from [3-Semesters](#3-semesters) as `semester_code`
- `code` from [5-Offerings](#5-offerings) as `offering_code`

### Data Export Manager Setup

- **Category:** Show All
- **Export From:**  `NQ com.txoof.brightspace.org.06sections`

**Labels Used on Export**

| Label |
|-|
|type|
|action|
|code|
|name|
|start_date|
|end_date|
|is_active|
|department_code|
|template_code|
|semester_code|
|offering_code|
|custom_code|

**Export Summary and Output Options**

- *Export File Name:* `6-Sections_Delete-%d.csv`
- *Line Delimiter:* `LF`
- *Field Delimiter:* `,`
- *Character Set:* `UTF-8`
- *Include Column Headers:* `True`

### Query Setup for `named_queries.xml`
| header | table.field | value | NOTE |
|-|-|-|-|
|type| CC.ID | _course offering_ | N1
|action| CC.ID | _DELETE_ | N1
|code| _'cs'\_schoolid\_coursenumber\_termid\_block\_sectionid_ | _cs\_3\_ITLDROB\_3101\_C\_12345_
|name| C.COURSE_NAME | _IT Robotics I - B Block (S2) Smith_
|start_date| CC.ID | '' | N1
|end_date| CC.ID | '' | N1
|is_active| CC.ID | '' | N1
|department_code| CC.ID | '' | N1
|template_code| CC.ID | '' | N1
|semester_code|   CC.ID | '' | N1
|offering_code| _'co'\_schoolid\_coursenumber\_termid_ | _co\_3\_ITLDROB\_3101_
|custom_code| CC.ID | '' | N1

**NOTES**

**N1:** Field does not appear in database; use a known field such as `<column column=STUDENT.ID>header<\column>` to prevent an "unknown column error"

**Tables Used**

| Table |
|-|
|STUDENTS|
|CC|
|TERMS|
|TEACHERS|
|SCHOOLSTAFF|
|COURSES|

**SQL**

```SQL
            -- 06 sections
            -- remove expired sections from previous school years
            select distinct
                'course section' as "type",
                'DELETE' as "action",
                /*
                use the following format to ensure that section codes are unique
                and remain constant even if the teacher is reassigned
                code: cs_3_SPHYIBS2_3200_D_28636
                */
                'cs_'||cc.schoolid||'_'||cc.course_number||'_'||cc.TermID||'_'||DECODE(regexp_replace(cc.expression, '[^0-9]', ''), 
                1, 'A', 
                2, 'B', 
                3, 'C', 
                4, 'D', 
                5, 'E', 
                6, 'F', 
                7, 'G', 
                8, 'H', 
                9, 'ADV',
                10, 'X',
                'UNKNOWN')||'_'||cc.sectionid as "code",
                /*
                use the following format to ensure that section names are unique 
                in each class; this will help differentiate sections when splitting classes
                section names: `SCI IB Physics SL Yr2 - A Block (22-23) Kremer`
                */
                c.course_name||' - '||DECODE(regexp_replace(cc.expression, '[^0-9]', ''), 
                1, 'A', 
                2, 'B', 
                3, 'C', 
                4, 'D', 
                5, 'E', 
                6, 'F', 
                7, 'G', 
                8, 'H', 
                9, 'ADV', 
                10, 'X', 
                'UNKNOWN')||' Block ('||terms.abbreviation||') '||teachers.last_name as "name",
                '' as "start_date",
                '' as "end_date",
                '' as "is_active",
                '' as "department_code",
                '' as "template_code",
                '' as "semester_code",
                'co_'||cc.schoolid||'_'||cc.course_number||'_'||cc.TermID as "offering_code",
                '' as "custom_code"
                '' as "start_date",
                '' as "end_date",
                '' as "is_active",
                '' as "department_code",
                '' as "template_code",
                '' as "semester_code",
                'co_'||cc.schoolid||'_'||cc.course_number||'_'||cc.TermID as "offering_code",
                '' as "custom_code"
            from 
            students s
            join cc on cc.studentid = s.id
            join schoolstaff ss on ss.id = cc.teacherid
            join teachers teachers on teachers.id = cc.teacherid
            join courses c on c.course_number = cc.course_number,
            terms terms
            where
                terms.id = cc.termid and
                /* select only courses that are in the previous yearid (e.g. 2021-2022 == 3100)*/
                cc.termid >= case 
                    when (EXTRACT(month from sysdate) >= 1 and EXTRACT(month from sysdate) <= 6)
                    THEN (EXTRACT(year from sysdate)-2000+8)*100
                    when (EXTRACT(month from sysdate) >= 7 and EXTRACT(month from sysdate) <= 12)
                    THEN (EXTRACT(year from sysdate)-2000+9)*100
                    end
                    and 
                    cc.termid < case
                    when (EXTRACT(month from sysdate) >= 1 and EXTRACT(month from sysdate) <= 6)
                    THEN (EXTRACT(year from sysdate)-2000+9)*100
                    when (EXTRACT(month from sysdate) >= 7 and EXTRACT(month from sysdate) <= 12)
                    THEN (EXTRACT(year from sysdate)-2000+10)*100
                    end
            order by "offering_code" desc
```