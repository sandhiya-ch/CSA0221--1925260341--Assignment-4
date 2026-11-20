#include <stdio.h>
#include <string.h>

#define MAX_ITEMS 20
#define MAX_SALES 20

struct Date {
    int day, month, year;
};

enum ItemType {
    PACKAGED,
    COOKED,
    COMBO
};

struct Item {
    int id;
    char name[30];
    float price;
    int stock;
    float revenue;
    enum ItemType type;

    union {
        struct Date expiry;
        char preparedTime[10];

        struct {
            int itemId[3];
            int quantity[3];
            int count;
        } combo;
    } details;
};

int findItem(struct Item items[], int n, int id) {
    for (int i = 0; i < n; i++) {
        if (items[i].id == id)
            return i;
    }
    return -1;
}

void recordSale(struct Item items[], int n, int id, int quantity) {
    int index = findItem(items, n, id);

    if (index == -1 || quantity <= 0) {
        printf("Invalid item or quantity!\n");
        return;
    }

    struct Item *p = &items[index];

    if (p->type == COMBO) {
        int available = 1;

        for (int i = 0; i < p->details.combo.count; i++) {
            int j = findItem(items, n,
                             p->details.combo.itemId[i]);

            if (j == -1 ||
                items[j].stock <
                p->details.combo.quantity[i] * quantity) {
                available = 0;
                break;
            }
        }

        if (!available) {
            printf("Insufficient stock for combo!\n");
            return;
        }

        for (int i = 0; i < p->details.combo.count; i++) {
            int j = findItem(items, n,
                             p->details.combo.itemId[i]);

            items[j].stock -=
                p->details.combo.quantity[i] * quantity;
        }
    } else {
        if (p->stock < quantity) {
            printf("Insufficient stock!\n");
            return;
        }

        p->stock -= quantity;
    }

    p->revenue += p->price * quantity;

    printf("Sale successful!\n");
    printf("Item: %s\n", p->name);
    printf("Total: Rs. %.2f\n", p->price * quantity);
}

int dateValue(struct Date d) {
    int days = d.year * 365;

    for (int i = 1; i < d.month; i++) {
        if (i == 2)
            days += 28;
        else if (i == 4 || i == 6 || i == 9 || i == 11)
            days += 30;
        else
            days += 31;
    }

    return days + d.day;
}

void expiryWarning(struct Item items[], int n,
                   struct Date today) {
    int current = dateValue(today);

    printf("\nExpiring Items:\n");

    for (int i = 0; i < n; i++) {
        if (items[i].type == PACKAGED) {
            int expiry = dateValue(items[i].details.expiry);

            if (expiry >= current && expiry <= current + 2) {
                printf("%s expires on %02d/%02d/%04d\n",
                       items[i].name,
                       items[i].details.expiry.day,
                       items[i].details.expiry.month,
                       items[i].details.expiry.year);
            }
        }
    }
}

void sortByRevenue(struct Item items[], int n) {
    struct Item temp;

    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (items[i].revenue < items[j].revenue) {
                temp = items[i];
                items[i] = items[j];
                items[j] = temp;
            }
        }
    }
}

void printSummary(struct Item items[], int n) {
    sortByRevenue(items, n);

    printf("\nDaily Revenue Summary:\n");
    printf("ID\tName\t\tRevenue\n");

    for (int i = 0; i < n; i++) {
        printf("%d\t%-15s Rs. %.2f\n",
               items[i].id,
               items[i].name,
               items[i].revenue);
    }
}

int main(void) {
    struct Item items[MAX_ITEMS] = {
        {
            .id = 1,
            .name = "Milk",
            .price = 30,
            .stock = 10,
            .revenue = 0,
            .type = PACKAGED,
            .details.expiry = {22, 11, 2026}
        },
        {
            .id = 2,
            .name = "Sandwich",
            .price = 50,
            .stock = 15,
            .revenue = 0,
            .type = COOKED,
            .details.preparedTime = "09:30"
        },
        {
            .id = 3,
            .name = "Juice",
            .price = 40,
            .stock = 8,
            .revenue = 0,
            .type = PACKAGED,
            .details.expiry = {21, 11, 2026}
        },
        {
            .id = 4,
            .name = "Combo Meal",
            .price = 100,
            .stock = 0,
            .revenue = 0,
            .type = COMBO,
            .details.combo = {
                {1, 2}, {1, 1}, 2
            }
        }
    };

    int n = 4;

    struct Date today = {20, 11, 2026};

    recordSale(items, n, 1, 2);
    recordSale(items, n, 2, 1);
    recordSale(items, n, 4, 1);
    recordSale(items, n, 1, 100);

    expiryWarning(items, n, today);

    printSummary(items, n);

    return 0;
}
