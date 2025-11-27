// ====================================================================
//  Listagem Escolar - Gerenciamento de Alunos, cursos e matriculas.
// ====================================================================     

        #include <stdio.h>
        #include <stdlib.h>
        #include <string.h>

// ======================================================
//  DEFINICAO DE STRUCTS
// ======================================================

typedef struct aluno {
    char nome[100];
    char endereco[200];
    char telefone[20];
    int idade;
    struct aluno *prox;
} Aluno;

typedef struct curso {
    char codigo[20];
    char nome[100];
    char instrutor[100];
    struct curso *prox;
} Curso;

typedef struct matricula {
    int numero;
    Aluno *aluno;
    Curso *curso;
    struct matricula *prox;
} Matricula;

// ======================================================
//  LISTAS GLOBAIS
// ======================================================

Aluno *listaAlunos = NULL;
Curso *listaCursos = NULL;
Matricula *listaMatriculas = NULL;
int numeroMatriculaGlobal = 1;

// ======================================================
//  FUNCAO DE ERRO
// ======================================================

static void reportar_erro(char *mensagem) {
    fprintf(stderr, "ERRO: %s\n", mensagem);
}

// ======================================================
//  FUNCOES DE BUSCA
// ======================================================

Aluno* buscarAluno(char *nome) {
    Aluno *a = listaAlunos;
    while (a != NULL) {
        if (strcmp(a->nome, nome) == 0)
            return a;
        a = a->prox;
    }
    return NULL;
}

Curso* buscarCurso(char *codigo) {
    Curso *c = listaCursos;
    while (c != NULL) {
        if (strcmp(c->codigo, codigo) == 0)
            return c;
        c = c->prox;
    }
    return NULL;
}

Matricula* buscarMatricula(int numero) {
    Matricula *m = listaMatriculas;
    while (m != NULL) {
        if (m->numero == numero)
            return m;
        m = m->prox;
    }
    return NULL;
}

// ======================================================
//  CRUD – ALUNO
// ======================================================

void cadastrarAluno() {
    char nome[100];
    printf("Nome: ");
    scanf(" %[^\n]", nome);

    if (buscarAluno(nome)) {
        reportar_erro("Aluno ja cadastrado!");
        return;
    }

    Aluno *novo = malloc(sizeof(Aluno));
    strcpy(novo->nome, nome);

    printf("Endereco: ");
    scanf(" %[^\n]", novo->endereco);

    printf("Telefone: ");
    scanf(" %[^\n]", novo->telefone);

    printf("Idade: ");
    scanf("%d", &novo->idade);

    novo->prox = listaAlunos;
    listaAlunos = novo;

    printf("Aluno cadastrado!\n");
}

void atualizarAluno() {
    char nome[100];
    printf("Nome do aluno a atualizar: ");
    scanf(" %[^\n]", nome);

    Aluno *a = buscarAluno(nome);
    if (!a) {
        reportar_erro("Aluno nao encontrado!");
        return;
    }

    printf("Novo endereco: ");
    scanf(" %[^\n]", a->endereco);

    printf("Novo telefone: ");
    scanf(" %[^\n]", a->telefone);

    printf("Nova idade: ");
    scanf("%d", &a->idade);

    printf("Aluno atualizado!\n");
}

void descadastrarAluno() {
    char nome[100];
    printf("Nome do aluno a remover: ");
    scanf(" %[^\n]", nome);

    Aluno *ant = NULL, *a = listaAlunos;

    while (a != NULL) {
        if (strcmp(a->nome, nome) == 0) break;
        ant = a;
        a = a->prox;
    }

    if (!a) {
        reportar_erro("Aluno nao encontrado!");
        return;
    }

    // caso queira remover matriculas desse aluno
    Matricula *m = listaMatriculas, *mant = NULL;
    while (m != NULL) {
        if (m->aluno == a) {
            if (mant) mant->prox = m->prox;
            else listaMatriculas = m->prox;
            free(m);
            m = (mant ? mant->prox : listaMatriculas);
            continue;
        }
        mant = m;
        m = m->prox;
    }

    if (ant) ant->prox = a->prox;
    else listaAlunos = a->prox;

    free(a);
    printf("Aluno removido!\n");
}

void procurarAluno() {
    char nome[100];
    printf("Nome: ");
    scanf(" %[^\n]", nome);

    Aluno *a = buscarAluno(nome);
    if (!a) {
        reportar_erro("Aluno nao encontrado!");
        return;
    }

    printf("Nome: %s\nEndereco: %s\nTelefone: %s\nIndade: %d\n",
           a->nome, a->endereco, a->telefone, a->idade);
}

// ======================================================
//  CRUD – CURSO
// ======================================================

void cadastrarCurso() {
    char codigo[20];
    printf("Codigo: ");
    scanf(" %[^\n]", codigo);

    if (buscarCurso(codigo)) {
        reportar_erro("Curso ja cadastrado!");
        return;
    }

    Curso *c = malloc(sizeof(Curso));
    strcpy(c->codigo, codigo);

    printf("Nome do curso: ");
    scanf(" %[^\n]", c->nome);

    printf("Instrutor: ");
    scanf(" %[^\n]", c->instrutor);

    c->prox = listaCursos;
    listaCursos = c;

    printf("Curso cadastrado!\n");
}

void atualizarCurso() {
    char codigo[20];
    printf("Codigo do curso: ");
    scanf(" %[^\n]", codigo);

    Curso *c = buscarCurso(codigo);
    if (!c) {
        reportar_erro("Curso nao encontrado!");
        return;
    }

    printf("Novo nome: ");
    scanf(" %[^\n]", c->nome);

    printf("Novo instrutor: ");
    scanf(" %[^\n]", c->instrutor);

    printf("Curso atualizado!\n");
}

void descadastrarCurso() {
    char codigo[20];
    printf("Codigo do curso: ");
    scanf(" %[^\n]", codigo);

    Curso *c = listaCursos, *ant = NULL;

    while (c != NULL) {
        if (strcmp(c->codigo, codigo) == 0) break;
        ant = c;
        c = c->prox;
    }

    if (!c) {
        reportar_erro("Curso nao encontrado!");
        return;
    }

            // remover as matriculas
    Matricula *m = listaMatriculas, *mant = NULL;
    while (m != NULL) {
        if (m->curso == c) {
            if (mant) mant->prox = m->prox;
            else listaMatriculas = m->prox;
            free(m);
            m = (mant ? mant->prox : listaMatriculas);
            continue;
        }
        mant = m;
        m = m->prox;
    }

    if (ant) ant->prox = c->prox;
    else listaCursos = c->prox;

    free(c);
    printf("Curso removido!\n");
}

void procurarCurso() {
    char codigo[20];
    printf("Codigo: ");
    scanf(" %[^\n]", codigo);

    Curso *c = buscarCurso(codigo);
    if (!c) {
        reportar_erro("Curso nao encontrado!");
        return;
    }

    printf("Codigo: %s\nNome: %s\nInstrutor: %s\n",
           c->codigo, c->nome, c->instrutor);
}

// ======================================================
//  MATRÍCULAS
// ======================================================

int contarAlunosNoCurso(Curso *curso) {
    int count = 0;
    Matricula *m = listaMatriculas;
    while (m != NULL) {
        if (m->curso == curso) count++;
        m = m->prox;
    }
    return count;
}

void matricularAluno() {
    char nome[100], codigo[20];
    printf("Nome do aluno: ");
    scanf(" %[^\n]", nome);

    Aluno *a = buscarAluno(nome);
    if (!a) {
        reportar_erro("Aluno inexistente!");
        return;
    }

    printf("Codigo do curso (ou enter para matricula automatica): ");
    fgets(codigo, sizeof(codigo), stdin); // pra limpar o buffer do scanf anterior
    fgets(codigo, sizeof(codigo), stdin);
    codigo[strcspn(codigo, "\n")] = 0;

    Curso *curso = NULL;

    if (strlen(codigo) == 0) {
        // matricula automática
        Curso *c = listaCursos;
        int menor = 999999;

        while (c) {
            int qtd = contarAlunosNoCurso(c);
            if (qtd < menor) {
                menor = qtd;
                curso = c;
            }
            c = c->prox;
        }

        if (!curso) {
            reportar_erro("Nao ha cursos cadastrados!");
            return;
        }
    } else {
        curso = buscarCurso(codigo);
        if (!curso) {
            reportar_erro("Curso inexistente!");
            return;
        }
    }

            // verifica se ja ta matriculado
    Matricula *m = listaMatriculas;
    while (m) {
        if (m->aluno == a && m->curso == curso) {
            reportar_erro("Aluno ja matriculado neste curso!");
            return;
        }
        m = m->prox;
    }

    Matricula *nova = malloc(sizeof(Matricula));
    nova->aluno = a;
    nova->curso = curso;
    nova->numero = numeroMatriculaGlobal++;
    nova->prox = listaMatriculas;
    listaMatriculas = nova;

    printf("Matricula realizada! Nº %d\n", nova->numero);
}

void procurarMatricula() {
    int num;
    printf("Numero da matricula: ");
    scanf("%d", &num);

    Matricula *m = buscarMatricula(num);
    if (!m) {
        reportar_erro("Matricula nao encontrada!");
        return;
    }

    printf("Matricula %d\nAluno: %s\nCurso: %s (%s)\n",
           m->numero, m->aluno->nome,
           m->curso->nome, m->curso->codigo);
}

void cancelarMatricula() {
    int num;
    printf("Numero da matricula: ");
    scanf("%d", &num);

    Matricula *m = listaMatriculas, *ant = NULL;

    while (m != NULL) {
        if (m->numero == num) break;
        ant = m;
        m = m->prox;
    }

    if (!m) {
        reportar_erro("Matricula nao encontrada!");
        return;
    }

    if (ant) ant->prox = m->prox;
    else listaMatriculas = m->prox;

    free(m);
    printf("Matricula cancelada!\n");
}

// ======================================================
//  LISTAGENS
// ======================================================

void listarMatriculas() {
    Matricula *m = listaMatriculas;
    while (m) {
        printf("Nº %d - %s -> %s\n", m->numero, m->aluno->nome, m->curso->nome);
        m = m->prox;
    }
}

void listarAlunos() {
    Aluno *a = listaAlunos;
    while (a) {
        printf("%s (%d anos)\n", a->nome, a->idade);
        a = a->prox;
    }
}

void listarCursos() {
    Curso *c = listaCursos;
    while (c) {
        printf("%s - %s (%s)\n", c->codigo, c->nome, c->instrutor);
        c = c->prox;
    }
}

void listarAlunosDeCurso() {
    char codigo[20];
    printf("Codigo do curso: ");
    scanf(" %[^\n]", codigo);

    Curso *c = buscarCurso(codigo);
    if (!c) {
        reportar_erro("Curso inexistente!");
        return;
    }

    Matricula *m = listaMatriculas;
    printf("Alunos do curso %s:\n", c->nome);

    while (m) {
        if (m->curso == c)
            printf("- %s\n", m->aluno->nome);
        m = m->prox;
    }
}

// (e qualquer outra listagem pode ser implementada de forma semelhante)


// ======================================================
//  ARQUIVOS BINARIOS
// ======================================================

void salvarDados() {
    FILE *fa = fopen("alunos.bin", "wb");
    FILE *fc = fopen("cursos.bin", "wb");
    FILE *fm = fopen("matriculas.bin", "wb");

    if (!fa || !fc || !fm) {
        reportar_erro("Erro ao salvar arquivos!");
        return;
    }

    // salvar alunos
    for (Aluno *a = listaAlunos; a != NULL; a = a->prox) {
        fwrite(a, sizeof(Aluno), 1, fa);
    }

    // salvar cursos
    for (Curso *c = listaCursos; c != NULL; c = c->prox) {
        fwrite(c, sizeof(Curso), 1, fc);
    }

    // salvar matrículas
    for (Matricula *m = listaMatriculas; m != NULL; m = m->prox) {
        // salvar apenas número + nomes
        fwrite(&m->numero, sizeof(int), 1, fm);
        fwrite(m->aluno->nome, sizeof(char), 100, fm);
        fwrite(m->curso->codigo, sizeof(char), 20, fm);
    }

    fclose(fa);
    fclose(fc);
    fclose(fm);

    printf("Dados salvos!\n");
}

void carregarDados() {
    FILE *fa = fopen("alunos.bin", "rb");
    FILE *fc = fopen("cursos.bin", "rb");
    FILE *fm = fopen("matriculas.bin", "rb");

    if (!fa || !fc || !fm) {
        printf("Nenhum dado carregado.\n");
        return;
    }

    // carregar alunos
    while (1) {
        Aluno temp;
        if (fread(&temp, sizeof(Aluno), 1, fa) != 1) break;
        Aluno *novo = malloc(sizeof(Aluno));
        *novo = temp;
        novo->prox = listaAlunos;
        listaAlunos = novo;
    }

    // carregar cursos
    while (1) {
        Curso temp;
        if (fread(&temp, sizeof(Curso), 1, fc) != 1) break;
        Curso *novo = malloc(sizeof(Curso));
        *novo = temp;
        novo->prox = listaCursos;
        listaCursos = novo;
    }

    // carregar matriculas
    while (1) {
        int numero;
        char nome[100];
        char codigo[20];

        if (fread(&numero, sizeof(int), 1, fm) != 1) break;
        fread(nome, sizeof(char), 100, fm);
        fread(codigo, sizeof(char), 20, fm);

        Aluno *a = buscarAluno(nome);
        Curso *c = buscarCurso(codigo);

        if (a && c) {
            Matricula *m = malloc(sizeof(Matricula));
            m->numero = numero;
            m->aluno = a;
            m->curso = c;
            m->prox = listaMatriculas;
            listaMatriculas = m;
        }
        if (numero >= numeroMatriculaGlobal)
            numeroMatriculaGlobal = numero + 1;
    }

    fclose(fa);
    fclose(fc);
    fclose(fm);

    printf("Dados carregados!\n");
}

// ======================================================
//  MENU
// ======================================================

void menu() {
    int opc;

    do {
        printf("\n========= MENU =========\n");
        printf("1. Cadastrar aluno\n");
        printf("2. Procurar aluno\n");
        printf("3. Atualizar aluno\n");
        printf("4. Descadastrar aluno\n");
        printf("5. Cadastrar curso\n");
        printf("6. Procurar curso\n");
        printf("7. Atualizar curso\n");
        printf("8. Descadastrar curso\n");
        printf("9. Matricular aluno\n");
        printf("10. Procurar matricula\n");
        printf("11. Cancelar matricula\n");
        printf("12. Listar matriculas\n");
        printf("13. Listar cursos\n");
        printf("14. Listar alunos\n");
        printf("15. Listar alunos de um curso\n");
        printf("16. Sair\n");
        printf("Opcao: ");
        scanf("%d", &opc);

        switch (opc) {
            case 1: cadastrarAluno(); break;
            case 2: procurarAluno(); break;
            case 3: atualizarAluno(); break;
            case 4: descadastrarAluno(); break;
            case 5: cadastrarCurso(); break;
            case 6: procurarCurso(); break;
            case 7: atualizarCurso(); break;
            case 8: descadastrarCurso(); break;
            case 9: matricularAluno(); break;
            case 10: procurarMatricula(); break;
            case 11: cancelarMatricula(); break;
            case 12: listarMatriculas(); break;
            case 13: listarCursos(); break;
            case 14: listarAlunos(); break;
            case 15: listarAlunosDeCurso(); break;
            case 16: salvarDados(); printf("Saindo...\n"); break;
            default: printf("Opcao invalida!\n");
        }

    } while (opc != 16);
}

// ======================================================
//  MAIN
// ======================================================

int main() {
    carregarDados();
    menu();
    return 0;
}
