# Desenvolvendo-um-Sistema-de-Gerenciamento-de-Pessoas-em-API-REST-com-Spring-Boot-

Desenvolver uma API REST com Spring Boot é um projeto excelente para aprender sobre sistemas de gerenciamento e também para adicionar ao seu portfólio. Vou detalhar o processo e fornecer exemplos práticos.

### Módulos do Projeto
O projeto pode ser dividido nos seguintes módulos:

1. **Configuração Inicial**: Configuração do projeto Spring Boot com as dependências necessárias.
2. **Modelo de Dados**: Definição das entidades que representam as pessoas na organização.
3. **Camada de Acesso a Dados (Repository)**: Uso do Spring Data para interação com o banco de dados.
4. **Camada de Serviço**: Lógica de negócios e serviços que operam sobre os dados.
5. **Camada de Controlador (Controller)**: Endpoints da API que expõem as funcionalidades do serviço.
6. **Integração com MapStruct**: Mapeamento automático entre entidades e DTOs.
7. **Testes**: Criação de testes unitários e de integração com Spring Test.
8. **Documentação**: Uso do Swagger ou SpringDoc para documentar a API.
9. **Segurança**: Implementação de segurança com Spring Security.
10. **Deploy**: Configuração e deploy da aplicação no Heroku.

### Exemplo Prático
Aqui está um exemplo simplificado de como você pode estruturar um dos módulos:

```java
// Modelo de Dados
@Entity
public class Pessoa {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    private String nome;
    private String cpf;
    // Getters e setters omitidos para brevidade
}

// Repository
public interface PessoaRepository extends JpaRepository<Pessoa, Long> {
}

// Serviço
@Service
public class PessoaService {
    @Autowired
    private PessoaRepository repository;
    
    public Pessoa salvarPessoa(Pessoa pessoa) {
        return repository.save(pessoa);
    }
}

// Controller
@RestController
@RequestMapping("/api/pessoas")
public class PessoaController {
    @Autowired
    private PessoaService service;
    
    @PostMapping
    public ResponseEntity<Pessoa> criarPessoa(@RequestBody Pessoa pessoa) {
        Pessoa novaPessoa = service.salvarPessoa(pessoa);
        return new ResponseEntity<>(novaPessoa, HttpStatus.CREATED);
    }
}
```

### Conceitos REST Envolvidos
- **Recursos**: Cada pessoa é um recurso que pode ser acessado através de um URI.
- **Métodos HTTP**: GET para leitura, POST para criação, PUT/PATCH para atualização e DELETE para exclusão.
- **Status HTTP**: Códigos de resposta adequados para cada operação (ex: 200 OK, 201 Created, 404 Not Found).
- **Representações**: Uso de JSON para representar os dados trocados entre cliente e servidor.

### Ferramentas Utilizadas
- **Spring Boot**: Para a criação rápida e fácil de aplicações Spring.
- **Spring Data**: Para a interação simplificada com o banco de dados.
- **MapStruct**: Para o mapeamento automático entre objetos Java.
- **Spring Test**: Para testar os componentes da aplicação.
- **Postman**: Para testar a API manualmente.
- **Heroku**: Para o deploy e hospedagem da aplicação na nuvem.

Espero que este resumo e exemplo prático, ajudem a quem precisar começar o projeto de gerenciamento de pessoas com Spring Boot.
