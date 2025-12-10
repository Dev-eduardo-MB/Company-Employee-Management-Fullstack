# About e Inicialização

Este sistema foi desenvolvido para realizar o gerenciamento de empresas e funcionários, permitindo criar, editar, listar e excluir registros com integração entre um front-end Angular e uma API REST Laravel.
Para iniciar o projeto, basta clonar o repositório:
```bash
https://github.com/Dev-eduardo-MB/Company-Employee-Management-Fullstack.git
```
após garantir que o `Docker` esteja instalado na máquina execute na raiz do projeto: 
```bash 
docker compose up -d
```
após isso, o front-end estará disponível na porta `4200` e o back-end Laravel na porta `8000`.

O projeto suporta relacionamento **N:N (muitos-para-muitos)** entre empresas e funcionários, permitindo:

- Um funcionário participar de várias empresas  
- Uma empresa possuir múltiplos funcionários  

---

##  Validações Principais

### **Empresas**
- Nome obrigatório  
- Endereço obrigatório  
- CNPJ obrigatório com **14 dígitos**  
- CNPJ único (sem duplicação)

### **Funcionários**
- Login único (somente letras, números, ponto e underline)  
- CPF com **11 dígitos** e único  
- E-mail validado e único  
- Senha com no mínimo **6 caracteres**  
- Senha automaticamente protegida com **bcrypt**

> Caso deseje enviar a senha sem hash, basta comentar o hashing no `EmployeeController`.

---

#  Tecnologias Utilizadas

## Front-end (Angular 21)
- Componentes standalone  
- Lazy loading de rotas  
- Services para comunicação HTTP  
- Páginas:
  - Listagem  
  - Criação  
  - Edição  
  - Detalhes  

---

## Back-end (Laravel)
- API REST completa  
- Estrutura MVC  
- Controllers com validações dedicadas  
- Models com relacionamento **N:N**  
- Tabela pivot: `company_employee`

---

#  API REST e Validações

A API segue estritamente o padrão REST usando:

- **GET**  
- **POST**  
- **PUT**  
- **DELETE**

---

## EmployeeController
- Valida login  
- Valida CPF (11 dígitos)  
- Valida e-mail  
- Verifica unicidade (com ignore nos updates)  
- Senha recebe **hash automático**

---

## CompanyController
- Valida nome  
- Valida endereço  
- CNPJ com 14 dígitos  
- Sincroniza funcionários via array de IDs enviado pelo front  

---

#  Services do Angular

Os services (`CompanyService` e `EmployeeService`) centralizam toda a comunicação com o backend.

Cada service possui métodos para:

- Listar  
- Criar  
- Atualizar  
- Remover  
- Buscar por ID  

A aplicação também utiliza uma função auxiliar `wrap()` para padronizar erros e respostas.

---

#  Rotas de Navegação

A aplicação utiliza rotas com `loadComponent` e estrutura modular.

### Rota inicial
- `/home`

### Funcionários
- `/employees` — listar  
- `/employees/new` — criar  
- `/employees/:id` — editar

### Empresas
- `/companies` — listar  
- `/companies/new` — criar  
- `/companies/:id` — editar  
- `/companies/:id/info` — detalhes

### Fallback
- `**` → redireciona para `/home`

