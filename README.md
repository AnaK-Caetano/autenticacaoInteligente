# Sistema de Autenticação Inteligente com Detecção de acesso suspeito

💡 Descrição:
Um sistema de login tradicional com autenticação por e-mail e senha, mas com um componente de IA que monitora os padrões de login dos usuários para identificar comportamentos suspeitos ou possível invasão de conta.

🛠 Funcionalidades básicas:
- Cadastro e login de usuários.
- Logs de login (IP, horário, dispositivo, localização).
- Detecção automática de comportamento atípico usando IA (ex: login de local incomum, em horário incomum, etc).
- Quando um comportamento é considerado anômalo, o sistema:
    - Envia uma notificação ao usuário.

### Diagrama de classes
```mermaid
classDiagram
    class User {
        +int id
        +String name
        +String email
        +String password
        +String passwordDigest
        +datetime createdAt
        +datetime updatedAt
    }

    class LoginAttempt {
        +Long id
        +int user_id(FK)
        +String ipAddress
        +String device
        +String location
        +LocalDateTime loginTime
        +boolean successful
        +boolean suspicious
        +SuspiciousActivity suspiciousActivity
    }

    class SuspiciousActivity {
        +Long id
        +String reason
        +String severity
        +boolean notifiedUser
    }

    class Alert {
        +Long id
        +String message
        +boolean seen
    }

    User "1" --> "*" LoginAttempt : has
    User "1" --> "*" Alert : has
    LoginAttempt "1" *-- "0..1" SuspiciousActivity : has
    SuspiciousActivity "1" --> "0..1" LoginAttempt : belongs to
```
