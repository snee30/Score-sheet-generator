#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<windows.h>

struct student_details{
    char name[31];
    int roll;
    int math, science, english, nepali, social;
};

void Add_Record(int);
void title_screen();
int check_roll(int);
void list_students();
void search_student();
void view_marksheet(int);
void delete_record(int);
void edit_record(int);

void draw_boundary(){
    int i;
    for(i=1; i<106; i++){
        printf("*");
    }
}

void draw_line(){ 
    int columns;
    CONSOLE_SCREEN_BUFFER_INFO csbi;
    int i;

    GetConsoleScreenBufferInfo(GetStdHandle(STD_OUTPUT_HANDLE), &csbi);
    columns = csbi.srWindow.Right - csbi.srWindow.Left + 1;
    for(i=0; i<columns; i++){
        printf("*");
    }
    //Stack_Overflow_Copied
}

int main(){

    title_screen();
    
    getchar();
    return 0;
}

void title_screen(){
    int choice_title, bulk_number;

    title_choose:
    printf("\n");
    draw_line();
    printf("\n\n[1] Add a Record");
    printf("\n[2] Add Bulk Records");
    printf("\n[3] List Students");
    printf("\n[4] Search Student");
    printf("\n[5] Quit");
    printf("\nWhat is your choice? : ");
    scanf("%d", &choice_title);
    fflush(stdin);

    switch(choice_title){
        case 1:
            printf("\n");
            draw_line();
            Add_Record(1);
            break;
        
        case 2:
            printf("\n");
            draw_line();
            printf("How Many Students? : ");
            scanf("%d%*c", &bulk_number);
            Add_Record(bulk_number);
            break;

        case 3:
            printf("\n");
            list_students();
            break;

        case 4:
            search_student();
            break;
        
        case 5:
            exit(1);
            break;

        default:
            printf("\n");
            draw_line();
            printf("\nBye Bye!!");
            title_screen();
            
    }
}

// CASE 1/ 2
void Add_Record(int n){
    
    struct student_details st[n];
    int i, x;

    for(i=0; i<n; i++){
        FILE *record_print = fopen("record.dat", "a");
        printf("\nEnter the information for student %d\n", i+1);
        fflush(stdin);

        printf("Enter Name: ");
        scanf("%[^\n]", st[i].name);
        fflush(stdin);

        re_rollno:
        printf("\nEnter Roll Number: ");
        scanf("%d", &st[i].roll);
        fflush(stdin);
        x = check_roll(st[i].roll);
        if(x!=0){
            printf("Roll Number Already Taken!! Try Another!!");
            goto re_rollno;
        }
        
        math_re_marks:
        printf("\nEnter Marks in Mathematics: ");
        scanf("%d", &st[i].math);
        fflush(stdin);
        if(st[i].math > 100){
            printf("Error! Full Marks is 100");
            goto math_re_marks;
        }

        science_re_marks:
        printf("\nEnter Marks in Science: ");
        scanf("%d", &st[i].science);
        fflush(stdin);
        if(st[i].science > 100){
            printf("Error! Full Marks is 100");
            goto science_re_marks;
        }

        english_re_marks:
        printf("\nEnter Marks in English: ");
        scanf("%d", &st[i].english);
        fflush(stdin);
        if(st[i].english > 100){
            printf("Error! Full Marks is 100");
            goto english_re_marks;
        }

        nepali_re_marks:
        printf("\nEnter Marks in Nepali: ");
        scanf("%d", &st[i].nepali);
        fflush(stdin);
        if(st[i].nepali > 100){
            printf("Error! Full Marks is 100");
            goto nepali_re_marks;
        }

        social_re_marks:
        printf("\nEnter Marks in Social: ");
        scanf("%d", &st[i].social);
        fflush(stdin);
        if(st[i].social > 100){
            printf("Error! Full Marks is 100");
            goto social_re_marks;
        }

        fprintf(record_print, "%s|%d|%d|%d|%d|%d|%d\n", st[i].name, st[i].roll, st[i].math, st[i].science, st[i].english, st[i].nepali, st[i].social);
        fclose(record_print);
        printf("\n");
    }
    title_screen();
}

//CASE 3
void list_students(){
    
    draw_line();
    struct student_details list;

    FILE *list_stu = fopen("record.dat", "r");
    printf("\n\tRoll\tName\n");
    while(fscanf(list_stu, "%[^|]|%d|%d|%d|%d|%d|%d\n", &list.name, &list.roll, &list.math, &list.science, &list.english, &list.nepali, &list.social) != EOF){
        printf("\t%d\t%s\n", list.roll, list.name);
    }

    fclose(list_stu);
    title_screen();
}

//CASE 4
void search_student(){
    int search_roll, flag = 0, list_choice;
    printf("\n");
    draw_line();
    
    printf("\nEnter Roll Number: ");
    scanf("%d", &search_roll);
    fflush(stdin);
    
    struct student_details search;

    FILE *search_file = fopen("record.dat", "r");
    while(fscanf(search_file, "%[^|]|%d|%d|%d|%d|%d|%d\n", &search.name, &search.roll, &search.math, &search.science, &search.english, &search.nepali, &search.social) != EOF){
        if(search.roll == search_roll){
            flag = 1;
            fclose(search_file);
            break;
        }
    }
    if(flag == 0){
        printf("\n");
        draw_line();
        printf("\nRoll Number Not Found!!");
        fclose(search_file);
        title_screen();
    }

    printf("\n");
    draw_line();
    printf("\nRecord Found!");
    printf("\nStudent Name: %s\n\n", search.name);
    draw_line();
    printf("\n[1] Edit Record\n[2] Delete Record\n[3] View Marksheet\n[4] Quit\nAny Other Key to Go Back\n\n");
    printf("What is Your Choice? : ");
    scanf("%d", &list_choice);
    fflush(stdin);

    switch(list_choice){
        case 1:
            edit_record(search.roll);
            break;

        case 2:
            delete_record(search.roll);
            break;

        case 3:
            view_marksheet(search.roll);
            break;

        case 4:
            exit(4);

        default:
            title_screen();
    }

}

void edit_record(int tbe_roll){
    struct student_details edit, delete;
    FILE *read = fopen("record.dat", "r");
    FILE *new = fopen("new.dat", "a");
    int edit_choose, x, continue_edit, per_roll;

    while(fscanf(read, "%[^|]|%d|%d|%d|%d|%d|%d\n", &edit.name, &edit.roll, &edit.math, &edit.science, &edit.english, &edit.nepali, &edit.social) != EOF){
        if(edit.roll == tbe_roll){
            per_roll = edit.roll;
            break;
        }
    }
    rewind(read);
    printf("\n");
    draw_line();
    printf("\nHello %s!\nYour Current Information is:\n\n", edit.name);
    printf("Name: %s\nRoll No: %d\nMarks in Mathematics: %d\nMarks in Science: %d\nMarks in English: %d\nMarks in Nepali: %d\nMarks in Social: %d", edit.name, edit.roll, edit.math, edit.science, edit.english, edit.nepali, edit.social);
    printf("\n\nWhich Information Do You Want to Edit? Choose From The Following:");
    printf("\n[1] Name\n[2] Roll No.\n[3] Marks in Mathematics\n[4] Marks in Science\n[5] Marks in English\n[6] Marks in Nepali\n[7] Marks in Social\nPress Any Other Key To Go Back");
    printf("\n\nChoose: ");
    scanf("%d", &edit_choose);
    fflush(stdin);

    switch(edit_choose){
        case 1:
        printf("Enter New Name: ");
        gets(edit.name);
        fflush(stdin);
        break;

        case 2:
        re_roll_edit:
        printf("Enter New Roll No: ");
        scanf("%d", &edit.roll);
        fflush(stdin);
        x = check_roll(edit.roll);
        if(x!=0){
            printf("Roll Number Already Taken!! Try Another!!");
            goto re_roll_edit;
        }
        break;

        case 3:
        edit_math:
        printf("Enter New Marks in Mathematics: ");
        scanf("%d", &edit.math);
        fflush(stdin);
        if(edit.math > 100){
            printf("Error! Full Marks is 100\n");
            goto edit_math;
        }
        break;

        case 4:
        edit_science:
        printf("Enter New Marks in Science: ");
        scanf("%d", &edit.science);
        fflush(stdin);
        if(edit.science > 100){
            printf("Error! Full Marks is 100\n");
            goto edit_science;
        }
        break; 

        case 5:
        edit_english:
        printf("Enter New Marks in English: ");
        scanf("%d", &edit.english);
        fflush(stdin);
        if(edit.english > 100){
            printf("Error! Full Marks is 100\n");
            goto edit_english;
        }
        break;

        case 6:
        edit_nepali:
        printf("Enter New Marks in Nepali: ");
        scanf("%d", &edit.nepali);
        fflush(stdin);
        if(edit.nepali > 100){
            printf("Error! Full Marks is 100\n");
            goto edit_nepali;
        }
        break;

        case 7:
        edit_social:
        printf("Enter New Marks in Social: ");
        scanf("%d", &edit.social);
        fflush(stdin);
        if(edit.social > 100){
            printf("Error! Full Marks is 100\n");
            goto edit_social;
        }
        break;
        
        default:
        remove("new.dat");
        title_screen();
    }
    
    while(fscanf(read, "%[^|]|%d|%d|%d|%d|%d|%d\n", &delete.name, &delete.roll, &delete.math, &delete.science, &delete.english, &delete.nepali, &delete.social) != EOF){
        if(delete.roll != per_roll){
            fprintf(new, "%s|%d|%d|%d|%d|%d|%d\n", delete.name, delete.roll, delete.math, delete.science, delete.english, delete.nepali, delete.social);
        }
        else{
            fprintf(new, "%s|%d|%d|%d|%d|%d|%d\n", edit.name, edit.roll, edit.math, edit.science, edit.english, edit.nepali, edit.social);
        }
    }
    fclose(read);
    fclose(new);
    remove("record.dat");
    rename("new.dat", "record.dat");

    re_choice_dn:
    printf("Edit Another Info?\n[1] Yes\n[2] No");
    printf("\nChoose : ");
    scanf("%d", &continue_edit);
    fflush(stdin);
    if(continue_edit == 1){
        edit_record(edit.roll);
    }
    else if(continue_edit == 2){
        title_screen();
    }
    else{
        printf("\nValue Out of Bounds!!");
        goto re_choice_dn;
    }
}

void delete_record(int tbd_roll){

    struct student_details delete;
    FILE *read = fopen("record.dat", "r");
    FILE *new = fopen("new.dat", "w");

    while(fscanf(read, "%[^|]|%d|%d|%d|%d|%d|%d\n", &delete.name, &delete.roll, &delete.math, &delete.science, &delete.english, &delete.nepali, &delete.social) != EOF){
        if(delete.roll != tbd_roll){
            fprintf(new, "%s|%d|%d|%d|%d|%d|%d\n", delete.name, delete.roll, delete.math, delete.science, delete.english, delete.nepali, delete.social);
        }
    }
    fclose(read);
    fclose(new);
    remove("record.dat");
    rename("new.dat", "record.dat");
    title_screen();
}

void view_marksheet(int tbc_roll){
    
    char name[31], *division;
    int roll, sub[5], i, total_marks = 0;

    FILE *search_file = fopen("record.dat", "r");
    while(fscanf(search_file, "%[^|]|%d|%d|%d|%d|%d|%d\n", &name, &roll, &sub[0], &sub[1], &sub[2], &sub[3], &sub[4]) != EOF){
        if(roll == tbc_roll){
            fclose(search_file);
            break;
        }
    }

    for(i=0; i<5; i++){
        total_marks += sub[i];
    }

    float per = (((float)total_marks / 500.0) * 100.0);

    for(i=0; i<5; i++){
        if (sub[i] < 38){
            division = "Fail";
            goto marksheet_creation;
        }
    }

    if(per >= 80)
        division = "Distinction";
    else if(per >= 70)
        division = "FIRST";
    else if(per >= 60)
        division = "SECOND";
    else if(per >= 50)
        division = "THIRD";
    else if(per >= 40)
        division = "FOURTH";
    else
        division = "Fail";


    int sn = 1;
 /******************* MARKSHEET CREATION **************************************/
    marksheet_creation:
    printf("\n");
    draw_line();
    printf("\n\nST. XAVIER'S COLLEGE");
    printf("\n\nSECOND TERM EXAMINATION\n\n");
    
    draw_boundary();
    printf("\n|\t\tName : %-81s|", name);
    printf("\n|\t\tRoll : %d\t\t\t\t\t\t\t\t\t\t|\n", roll);
    
    draw_boundary();
    printf("\n|\tS.N\t|\t\t\tSubjects\t\t|\t\tMarks\t\t\t|\n");
    draw_boundary();
    printf("\n|\t%d.\t|\t\t\tMathematics\t\t|\t\t%d\t\t\t|", sn, sub[0]);
    printf("\n|\t%d.\t|\t\t\tScience\t\t\t|\t\t%d\t\t\t|", (sn+1), sub[1]);
    printf("\n|\t%d.\t|\t\t\tEnglish\t\t\t|\t\t%d\t\t\t|", (sn+2), sub[2]);
    printf("\n|\t%d.\t|\t\t\tNepali\t\t\t|\t\t%d\t\t\t|", (sn+3), sub[3]);
    printf("\n|\t%d.\t|\t\t\tSocial\t\t\t|\t\t%d\t\t\t|\n", (sn+4), sub[4]);

    draw_boundary();
    printf("\n|\t \t|\t\t\tPercentage\t\t|\t\t%.2f%%\t\t\t|", per);
    printf("\n|\t \t|\t\t\tDivision\t\t|\t\t%-11s\t\t|\n", division);
    
    draw_boundary();
    printf("\n\nEND OF RESULT\n");
    title_screen();
}

int check_roll(int roll){
    struct student_details st;

    FILE *roll_check = fopen("record.dat", "r");
    while(fscanf(roll_check, "%[^|]|%d|%d|%d|%d|%d|%d\n", &st.name, &st.roll, &st.math, &st.science, &st.english, &st.nepali, &st.social) != EOF){
        if(st.roll == roll){
            fclose(roll_check);
            return 1;
        }
    }
    fclose(roll_check);
    return 0;
}
