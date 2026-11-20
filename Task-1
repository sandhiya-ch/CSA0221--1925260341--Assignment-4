#include <stdio.h>
#include <string.h>

struct Date {
    int day, month, year;
};

struct BP {
    int systolic, diastolic;
};

struct Patient {
    char name[50];
    int age;
    char phone[11];
    struct BP bp;
    struct Date visitDate;
};

void addPatient(struct Patient *p, char n[], int a, char ph[],
                int s, int d, int day, int month, int year) {
    strcpy(p->name, n);
    p->age = a;
    strcpy(p->phone, ph);
    p->bp.systolic = s;
    p->bp.diastolic = d;
    p->visitDate.day = day;
    p->visitDate.month = month;
    p->visitDate.year = year;
}

int main() {
    struct Patient p;

    addPatient(&p, "Sandhiya", 18, "9876543210",
               120, 80, 20, 11, 2026);

    printf("Name: %s\n", p.name);
    printf("Age: %d\n", p.age);
    printf("Phone: %s\n", p.phone);
    printf("Blood Pressure: %d/%d\n",
           p.bp.systolic, p.bp.diastolic);
    printf("Visit Date: %02d/%02d/%d\n",
           p.visitDate.day, p.visitDate.month,
           p.visitDate.year);

    return 0;
}
