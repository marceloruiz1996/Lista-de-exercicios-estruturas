#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>

typedef struct {
    char nome[100];
    int idade;
    char endereco[100];
} Pessoa;

void exercicio1() {
    Pessoa p;
    scanf(" %[^"]", p.nome);
    scanf("%d", &p.idade);
    scanf(" %[^"]", p.endereco);
    printf("%s\n%d\n%s\n", p.nome, p.idade, p.endereco);
}

typedef struct {
    float x, y;
} Ponto;

void exercicio2() {
    Ponto p;
    scanf("%f %f", &p.x, &p.y);
    printf("%.2f\n", sqrt(p.x * p.x + p.y * p.y));
}

void exercicio3() {
    Ponto p1, p2;
    scanf("%f %f", &p1.x, &p1.y);
    scanf("%f %f", &p2.x, &p2.y);
    printf("%.2f\n", sqrt(pow(p2.x - p1.x, 2) + pow(p2.y - p1.y, 2)));
}

typedef struct {
    Ponto sup_esq;
    Ponto inf_dir;
} Retangulo;

void exercicio4() {
    Retangulo r;
    scanf("%f %f", &r.sup_esq.x, &r.sup_esq.y);
    scanf("%f %f", &r.inf_dir.x, &r.inf_dir.y);
    float base = fabs(r.inf_dir.x - r.sup_esq.x);
    float altura = fabs(r.sup_esq.y - r.inf_dir.y);
    float area = base * altura;
    float diagonal = sqrt(base * base + altura * altura);
    float perimetro = 2 * (base + altura);
    printf("%.2f %.2f %.2f\n", area, diagonal, perimetro);
}

void exercicio5() {
    Retangulo r;
    Ponto p;
    scanf("%f %f", &r.sup_esq.x, &r.sup_esq.y);
    scanf("%f %f", &r.inf_dir.x, &r.inf_dir.y);
    scanf("%f %f", &p.x, &p.y);
    if (p.x >= r.sup_esq.x && p.x <= r.inf_dir.x && p.y <= r.sup_esq.y && p.y >= r.inf_dir.y)
        printf("Dentro\n");
    else
        printf("Fora\n");
}

typedef struct {
    int matricula;
    char nome[100];
    float notas[3];
} Aluno;

void exercicio6() {
    Aluno alunos[5];
    float maior_media = 0;
    int index = 0;
    for (int i = 0; i < 5; i++) {
        scanf("%d", &alunos[i].matricula);
        scanf(" %[^"]", alunos[i].nome);
        for (int j = 0; j < 3; j++) scanf("%f", &alunos[i].notas[j]);
        float media = (alunos[i].notas[0] + alunos[i].notas[1] + alunos[i].notas[2]) / 3.0;
        if (media > maior_media) {
            maior_media = media;
            index = i;
        }
    }
    printf("%s %.2f %.2f %.2f\n", alunos[index].nome,
        alunos[index].notas[0], alunos[index].notas[1], alunos[index].notas[2]);
}

typedef struct {
    int h, m, s;
} Hora;

void exercicio7() {
    Hora h[5], maior = {0, 0, 0};
    for (int i = 0; i < 5; i++) scanf("%d %d %d", &h[i].h, &h[i].m, &h[i].s);
    for (int i = 1; i < 5; i++) {
        if ((h[i].h > maior.h) ||
            (h[i].h == maior.h && h[i].m > maior.m) ||
            (h[i].h == maior.h && h[i].m == maior.m && h[i].s > maior.s)) {
            maior = h[i];
        }
    }
    printf("%02d:%02d:%02d\n", maior.h, maior.m, maior.s);
}

typedef struct {
    int dia, mes, ano;
} Data;

typedef struct {
    char nome[100];
    Data nasc;
} PessoaData;

void exercicio8() {
    PessoaData pessoas[6];
    int mais_nova = 0, mais_velha = 0;
    for (int i = 0; i < 6; i++) {
        scanf(" %[^"]", pessoas[i].nome);
        scanf("%d %d %d", &pessoas[i].nasc.dia, &pessoas[i].nasc.mes, &pessoas[i].nasc.ano);
    }
    for (int i = 1; i < 6; i++) {
        Data a = pessoas[i].nasc;
        Data v = pessoas[mais_velha].nasc;
        if (a.ano < v.ano || (a.ano == v.ano && a.mes < v.mes) || (a.ano == v.ano && a.mes == v.mes && a.dia < v.dia))
            mais_velha = i;
        if (a.ano > pessoas[mais_nova].nasc.ano || (a.ano == pessoas[mais_nova].nasc.ano && a.mes > pessoas[mais_nova].nasc.mes) || (a.ano == pessoas[mais_nova].nasc.ano && a.mes == pessoas[mais_nova].nasc.mes && a.dia > pessoas[mais_nova].nasc.dia))
            mais_nova = i;
    }
    printf("%s\n%s\n", pessoas[mais_velha].nome, pessoas[mais_nova].nome);
}

typedef struct {
    char nome[100];
    char esporte[50];
    int idade;
    float altura;
} Atleta;

void exercicio9() {
    Atleta atletas[5];
    int mais_alto = 0, mais_velho = 0;
    for (int i = 0; i < 5; i++) {
        scanf(" %[^"]", atletas[i].nome);
        scanf(" %[^"]", atletas[i].esporte);
        scanf("%d %f", &atletas[i].idade, &atletas[i].altura);
    }
    for (int i = 1; i < 5; i++) {
        if (atletas[i].altura > atletas[mais_alto].altura) mais_alto = i;
        if (atletas[i].idade > atletas[mais_velho].idade) mais_velho = i;
    }
    printf("%s\n%s\n", atletas[mais_alto].nome, atletas[mais_velho].nome);
}

void exercicio10() {
    Atleta atletas[5], temp;
    for (int i = 0; i < 5; i++) {
        scanf(" %[^"]", atletas[i].nome);
        scanf(" %[^"]", atletas[i].esporte);
        scanf("%d %f", &atletas[i].idade, &atletas[i].altura);
    }
    for (int i = 0; i < 4; i++) {
        for (int j = i + 1; j < 5; j++) {
            if (atletas[i].idade < atletas[j].idade) {
                temp = atletas[i];
                atletas[i] = atletas[j];
                atletas[j] = temp;
            }
        }
    }
    for (int i = 0; i < 5; i++) {
        printf("%s %s %d %.2f\n", atletas[i].nome, atletas[i].esporte, atletas[i].idade, atletas[i].altura);
    }
}

int contarDias(Data d1, Data d2) {
    int dias1 = d1.ano * 365 + d1.mes * 30 + d1.dia;
    int dias2 = d2.ano * 365 + d2.mes * 30 + d2.dia;
    return abs(dias2 - dias1);
}

void exercicio11() {
    Data d1, d2;
    scanf("%d %d %d", &d1.dia, &d1.mes, &d1.ano);
    scanf("%d %d %d", &d2.dia, &d2.mes, &d2.ano);
    printf("%d\n", contarDias(d1, d2));
}

int main() {
    int op;
    do {
        scanf("%d", &op);
        switch(op) {
            case 1: exercicio1(); break;
            case 2: exercicio2(); break;
            case 3: exercicio3(); break;
            case 4: exercicio4(); break;
            case 5: exercicio5(); break;
            case 6: exercicio6(); break;
            case 7: exercicio7(); break;
            case 8: exercicio8(); break;
            case 9: exercicio9(); break;
            case 10: exercicio10(); break;
            case 11: exercicio11(); break;
        }
    } while(op != 0);
    return 0;
}
