#include <stdio.h>

/* Static storage class */
int next_token(void) {
    static int token = 1000;
    return ++token;
}

/* Automatic storage class */
int auto_token(void) {
    int token = 1000;
    return ++token;
}

/* Global variable with extern */
int global_token = 1000;

int extern_token(void) {
    extern int global_token;
    return ++global_token;
}

/* Register storage class */
void print_tokens(void) {
    for (register int i = 1001; i <= 1003; i++) {
        printf("%d ", i);
    }
    printf("\n");
}

int main(void) {
    int s1 = next_token();
    int s2 = next_token();
    int s3 = next_token();

    int a1 = auto_token();
    int a2 = auto_token();
    int a3 = auto_token();

    int e1 = extern_token();
    int e2 = extern_token();
    int e3 = extern_token();

    printf("Static: %d %d %d\n", s1, s2, s3);
    printf("Auto: %d %d %d\n", a1, a2, a3);
    printf("Extern: %d %d %d\n", e1, e2, e3);

    printf("Register: ");
    print_tokens();

    return 0;
}
