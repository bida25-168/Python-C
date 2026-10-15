# Grade book Management System
## Python Program Sections A-D


###Section A 
Purpose: To accep user input, display outputs and process scalar data
How??: The program initially asks the user for the total number of students they intend to record data on . To accommodate for the different data that will be recorded they were divided into lists for the grades and thestudents themselves
For the grades they had to be between 0 and 100 and therefore operators we're used to ensure these conditions are met before any other calculations can be done and if not met the user is prompted to enter the correct data.
The correct data is then added to the end of the list students

With the grades entered the program uses mathematical operators and expressions to calculate the sum of marks and the class average and in the end showing all this data in an organised report.

####Section A
number_of_students = int(input("Please enter the total number of students: "))
grade = []
students = []
for _ in range(number_of_students):
    name = input("Please enter student name: ")
    subject = input("Please enter subject name: ")
    marks = float(input("Please enter the subjects grade: "))
    while True:
        grade = int(input("Please enter the subjects grade:" ))
        if grade <=0 or grade >= 100:
            break
        print("Please enter a value between 0 and 100")
    students.append((name,grade))
class_total = sum(marks)
class_avg = class_total / number_of_students
for student in students:
     print(f"Name:",{name},"Grade: ", {marks}, "Class Average: ", {class_avg} )


Output: The report showing the Name, grade and class average

###Section B
Purpose: Change list into tuple to handle multipe records
How??
In order to expand the data that was already entered in Section A, it is important that the Management system allows one to enter names of students and their 3 subjects until range is filled. This was done by iterating over the empty lists to enter data for those students and subjects while ensuring that they fall within the expected conditions range.
For the grades a separate variable was used hich was then added to the end of the students_other to create the list of tuples that show the students and the grades they obtained.
Further more the program calculated the students average for all the grades and also the lowest, highest marks in subjects respectively.

Output: The program displays the highest and lowest grades (using aggregation e.g maxmin), the table to show students names, grades and average.

# Section B

students_other = []
for _ in range(number_of_students):
    name = input("Please enter student name: ")
    subject_grades = []

    for subject in ("MATH", "ENG", "SCIENCE"):
        while True:
            g = float(input(f"Please enter the {subject} grade:"))
            if g <=0 or g >= 100:
                subject_grades.append(g)
                break
            print("Please enter a value between 0 and 100")
    students_other.append((name,subject_grades))

for name,grade in students_other:
    print(f"Name:{name} , Math Grade:{grade[0]}, English Grade:{grade[1]}, Science Grade:{grade[2]}")

for name,grades in students_other:
    std_avg = sum(grades) / len(grades)
    print(f"Name,{name}, "f"Avgerage mark:,{std_avg}")

high_maths = max(student[0] for name,student in students_other)
print(f"Highest In Math:,{high_maths}")

high_english = max(student[1] for name,student in students_other)
print(f"Highest In English:,{high_english}")
high_Science = max(student[2] for name,student in students_other)
print(f"Highest In Science:,{high_Science}")
low_maths = min(student[0] for name,student in students_other)
print(f"Lowest In Math:,{low_maths}")
low_english = min(student[1] for name,student in students_other)
print(f"Lowest In English:,{low_english}")
low_Science = min(student[2] for name,student in students_other)
print(f"Lowest In Science:,{low_Science}")


print(f"{'Name',:<10 }{'Math':>6} {'English Grade': >8}{'Science Grade': >8}{'Avgerage mark': >8}")
print("-" * 44)

for name,grades in students_other:
    std_average = sum(grades) / len(grades)
    print(f"{name:<10 }{grades[0]:>6} {grades[1] >8}{grades[2] >8}{std_average: >8.2f}")
    print("-" * 44) # prints dashed line 44 characters long


### Section C 
#####Purpose : Change list of tuples into dictionary
#####How?? In order to link the variables and data in the other program file the list of tuples had to be imported at the start of the program . A new empty dictionary was created(student_dict) to store the keys( names) as a separate dictionary and the values(grades) as a separate dictionary as well.
#####Main Functions : def_add_student(name, grade)
                ~def update_student(name, grade)
                ~def remove student (name)
* If value or key is absent the program notifies the user.
Other Functions ~ def search_student(name) to allow the user to look for a specific person within out dataset to reveal sll their other data.


from Section_a_and_b import  students_other #Imports tuple
student_dict = {}
for name,grade in students_other:
    student_dict[name] = {'grades':grade}

def add_student(name,grades):
    student_dict[name] = {'grades':grades}

def update_student(name,grades):
    if name in student_dict:
     student_dict[name] = {'grades':grades}
    else:
        print("Student with name '{}' does not exist".format(name))

def remove_student(name):
    if name in student_dict:
        del student_dict[name]
    else:
        print("Student with name '{}' does not exist".format(name))

subject_dict = {}
for name,grades in students_other:
    for subject,grade in zip(("MATH", "ENG", "SCIENCE"),grade): # Pairs iterables grade and subject names side by side
        subject_dict.setdefault(subject,[]).append(grade)

choice = input("Please enter a subject either MATH/ENG/SCIENCE:  ").upper()
if choice in subject_dict:
    print(f"Grades for {choice}: {subject_dict[choice]}")
else:
    print(f"Subject {choice} does not exist")

def search_student(name):
    """Returns the data name for a matching student else None."""
    for student_name, grades in student_dict.items():
        if student_name.lower() == name.lower():
            return student_name , grades
    return None

while True:
     print(f"      Search Here      ")
     feature = input("Enter the name you want to search(or 'quit' to exit): ")
     if feature.lower() == 'quit':
         break
     found = search_student(feature)
     if found:
         student_name,grades= found
         grade = grades['grades']
         average = sum(grade)/len(grade)
         print(
             f"Found: {student_name} | "
             f"Maths:{grade[0]} | English{grade[1]} | Science: {grade[2]} "
             f"Average: {average:.2f}")
     else:
         print(f"No student found with the name {feature}")

### SECTION D
#####Purpose: The sole reason behind the logic in this section is to combine the logic from the different codes in sections a,b and c in order to modularize them into functions to allow for error handling and adding functionality to the program.

#####How?? The code makes use of the add_student(), avg_student(), display_student(), student_summary and 
update_student() functions . Where:
   - add_student() : the function accepts five parameters being : name, gradebook, maths, english and science grades      This provides a complete record for a student into an empty dictionary (gradebook).This function is to recieve data as parameters and does not display them.
   - avg_student() : the function accepts one parameter , name. This allows it to access the grades for the subjects        in order to find the students average grade. This function calculates the average grade of the students.
   
   - display_student : The function takes the name of the student and the dictionary it is found in to be able to           provide details about a single student. It shows their name , grade for respective subjects and average grade          .This functions accepts inputs in order to print the output  or results being the students grades,their average        and their name.
   
   - student_summary(): The function accepts a single parameter being the dictionary name to be able to look into it       for the name and grade of each student to provide the average as a summary for all students entered in the             dictionary.This function works to perform neccessary calculations in order to display the results .
   
   - update_student(): it accepts two parameters being gradebook and the name in order to loop through the dictionary      to find the details for a student using their name in order to make changes to their grades for each subject.          This function works to modify the data then display it after making changes.

Importance: Modularization allows for various code to be used many times within the program without having to re-write code again this is evident as the avg_student() function is called in other functions in the program to avoid duplicating its logic. While enforcing re-usability it allows for bugs to be detected easily as the error will be found and easy fixed as they are smaller problems of the main problem. Hence making debugging easy.
Making use of docstrings in every function ensures that when program is being implemented the expected outputs and inputs and purpose of each function is know in order to make it easy to understand them and subsequently how they work together.
Re

#####Search and Update Function in Detail
Parameter: name , gradebook
Having accepted the name of the student as a parameter in order to standardise the way they are represented, .upper() converts to uppercase text .The program then checks if the name exists in the dictionary, if not the user is notified and if not the user is prompted to enter the new grades for subjects respectively.

As the grades are different from the original ones new variables are created for them and to validate the data being entered, assertion is used to check that the grades fall within an acceptable range and if the values entered are  numerical. Existence of these errors prompts the user to correct by entering the correct data or range.

For Example: 
Enter student name: Tabetha
Student 'TABETHA' does not exist

Enter student name: YOlice
Enter the new maths grade: 85
Enter the new english grade: 90
Enter the new science grade: 78
Student YOLICE has been successfully updated!

#####Error- Handling
- ValueError : This works to catch errors that have to deal with data entered not being numeric where it is supposed to be. It also deals with catching errors that have to do with empty strings. Evident in the add_student() and update_student() functions.
- AssertionError: This works to catch errors that involve the wrong range of values having been entered into the dictionary. Evident in the add_student() and update_student() functions where the grades have to be numbers between zero and one-hundred
- ZeroDivisionError: This except works to catch an error whereby the denominator is zero and prevents the program from crashing . This is evident in the avg_student() function that prints a message in cases where the student has no grades to act as a defensive check.

- 


