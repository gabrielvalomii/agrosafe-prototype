# AgroSafe - Sistema de Controle de Acesso por Reconhecimento Facial

## 📋 Visão Geral

AgroSafe é uma aplicação web de controle de acesso integrada desenvolvida para gerenciar e verificar a entrada de visitantes em propriedades agrícolas através de reconhecimento facial e autenticação segura. O projeto é composto por um **backend Django REST API** e um **frontend React moderno**, ambos containerizados com Docker.

## 🎯 Objetivo

Proporcionar um sistema seguro e eficiente para monitorar e controlar o acesso a áreas protegidas, utilizando tecnologias de reconhecimento facial (OpenCV) integradas com um portal web responsivo.

---

## 🏗️ Arquitetura do Projeto

### Backend (Django)
- **Localização**: `./agroSafe/`
- **Tecnologias**: Python, Django, Django REST Framework
- **Banco de Dados**: SQLite
- **Reconhecimento Facial**: OpenCV
- **Port**: 8000

### Frontend (React + TypeScript)
- **Localização**: `./agrosafe-mvp-frontend/`
- **Tecnologias**: React, TypeScript, Vite, Zustand (State Management)
- **Build Tool**: Vite
- **Port**: 5173

### Containerização
- **Docker Compose**: Orquestra os serviços backend e frontend
- Ambos os serviços possuem `Dockerfile` para isolamento de ambiente

---

## 📁 Estrutura do Projeto

```
agrosafe-prototype/
├── docker-compose.yml              # Orquestração dos serviços
├── README.MD                        # Este arquivo
├── agroSafe/                        # Backend Django
│   ├── Dockerfile                  # Container do backend
│   ├── requirements.txt            # Dependências Python
│   ├── README.md                   # Documentação do backend
│   └── agroSafe/                   # Aplicação Django
│       ├── manage.py               # CLI do Django
│       ├── db.sqlite3              # Banco de dados
│       ├── appbk/                  # App principal
│       │   ├── models.py           # Modelos de dados
│       │   ├── views.py            # Views principais
│       │   ├── views_porteiro.py   # Views do porteiro
│       │   ├── views_visitante.py  # Views do visitante
│       │   ├── urls.py             # Rotas da API
│       │   ├── face_opencv.py      # Integração com OpenCV
│       │   ├── settings.py         # Configurações
│       │   ├── admin.py            # Admin Django
│       │   ├── apps.py             # Configuração da app
│       │   ├── asgi.py             # ASGI config
│       │   ├── wsgi.py             # WSGI config
│       │   ├── migrations/         # Migrações do banco
│       │   └── tests.py            # Testes
│       └── static/                 # Arquivos estáticos
│           └── main/
│               ├── script.js
│               └── style.css
└── agrosafe-mvp-frontend/          # Frontend React
    ├── Dockerfile                  # Container do frontend
    ├── package.json                # Dependências Node.js
    ├── vite.config.ts              # Configuração Vite
    ├── tsconfig.json               # Configuração TypeScript
    ├── index.html                  # HTML principal
    └── src/
        ├── main.tsx                # Ponto de entrada React
        ├── App.tsx                 # Componente raiz
        ├── index.css               # Estilos globais
        ├── theme.ts                # Tema e configurações UI
        ├── router.tsx              # Configuração de rotas
        ├── api/                    # Integração com API
        │   ├── auth.ts             # Endpoints de autenticação
        │   └── visitors.ts         # Endpoints de visitantes
        ├── components/             # Componentes reutilizáveis
        │   ├── navbar.tsx
        │   ├── page-base.tsx
        ├── hooks/                  # Custom React hooks
        │   ├── use-auth.ts         # Hook de autenticação
        │   └── use-visitors.ts     # Hook de visitantes
        ├── pages/                  # Páginas da aplicação
        │   ├── login/              # Página de login
        │   ├── register/           # Página de registro
        │   └── access-verification/# Página de verificação
        ├── stores/                 # Gerenciamento de estado (Zustand)
        │   ├── auth.ts             # Store de autenticação
        │   └── use-temp-image-store.ts
        ├── lib/
        │   └── api.ts              # Configuração e cliente API
        └── assets/                 # Imagens e recursos
```

---

## 🔧 Dependências

### Backend
- Django
- Django REST Framework
- OpenCV (cv2)
- Pillow (manipulação de imagens)
- Cors Headers (CORS)
- Python Decouple (variáveis de ambiente)

### Frontend
- React 18+
- TypeScript
- Vite
- Zustand (gerenciamento de estado)
- TanStack Query (cache de dados)
- React Router (roteamento)

---

## ⚙️ Configuração e Instalação

### Pré-requisitos
- Docker e Docker Compose instalados
- Python 3.9+ (para desenvolvimento local)
- Node.js 18+ (para desenvolvimento local)

### Usando Docker Compose (Recomendado)

```bash
# Clonar o repositório
git clone <repositório>
cd agrosafe-prototype

# Iniciar os serviços
docker-compose up -d

# Verificar logs
docker-compose logs -f

# Parar os serviços
docker-compose down
```

**Acesso**:
- Frontend: http://localhost:5173
- Backend API: http://localhost:8000
- Admin Django: http://localhost:8000/admin

### Desenvolvimento Local

#### Backend
```bash
cd agroSafe

# Criar ambiente virtual
python -m venv venv

# Ativar ambiente (Windows)
venv\Scripts\activate
# Ativar ambiente (Linux/Mac)
source venv/bin/activate

# Instalar dependências
pip install -r requirements.txt

# Aplicar migrações
python agroSafe/manage.py migrate

# Criar superuser
python agroSafe/manage.py createsuperuser

# Iniciar servidor
python agroSafe/manage.py runserver
```

#### Frontend
```bash
cd agrosafe-mvp-frontend

# Instalar dependências
npm install

# Iniciar desenvolvimento
npm run dev

# Build para produção
npm run build

# Preview do build
npm run preview
```

---

## 📡 API REST - Endpoints Principais

### Autenticação
- `POST /api/auth/login` - Login de usuário
- `POST /api/auth/register` - Registro de novo usuário
- `POST /api/auth/logout` - Logout

### Visitantes
- `GET /api/visitors/` - Listar visitantes
- `POST /api/visitors/` - Registrar novo visitante
- `GET /api/visitors/{id}/` - Obter detalhes do visitante
- `PUT /api/visitors/{id}/` - Atualizar visitante
- `DELETE /api/visitors/{id}/` - Deletar visitante

### Controle de Acesso
- `POST /api/access/verify` - Verificar acesso com reconhecimento facial
- `GET /api/access/logs/` - Listar logs de acesso
- `POST /api/access/manual-verification` - Verificação manual

### Porteiros
- `GET /api/porteiros/` - Listar porteiros
- `POST /api/porteiros/` - Registrar porteiro
- `GET /api/porteiros/{id}/` - Obter detalhes do porteiro

---

## 🎨 Páginas e Funcionalidades

### Página de Login
- Autenticação com email/CPF
- Validação de credenciais
- Persistência de sessão

### Página de Registro
- Cadastro de novo usuário
- Validação de dados
- Upload de foto/captura de câmera

### Verificação de Acesso
- **Camera Feed Panel**: Captura de vídeo em tempo real
- **Reconhecimento Facial**: Integração com OpenCV
- **Manual Verification Modal**: Verificação manual de visitantes
- **Zoomable Image**: Visualização de fotos com zoom

---

## 🔐 Autenticação e Segurança

- Autenticação baseada em token JWT
- Senhas criptografadas (hash)
- CORS configurado para comunicação entre front e back
- Validação de dados em ambos os lados

---

## 📊 Modelos de Dados

### Pessoa
- ID (UUID)
- Nome
- Email
- CPF
- Telefone
- Senha (hash)

### Visitante
- Pessoa (FK)
- Data de visita
- Motivo da visita
- Foto/Hash da foto
- Base64 da imagem

### Cadastro Visitante Portaria
- Visitante
- Empresa/Granja (nivel)
- Foto
- Foto Base64

### Registro de Acesso Portaria
- Visitante/Porteiro
- Timestamp do acesso
- Status (aprovado/negado)
- Motivo (se negado)
- Observação

---

## 🔄 Fluxo de Funcionamento

1. **Usuário acessa o frontend** (http://localhost:5173)
2. **Login/Registro**: Autenticação no backend
3. **Verificação de Acesso**: 
   - Usuário autorizado captura foto/vídeo
   - OpenCV processa reconhecimento facial
   - Backend verifica se visitante está cadastrado
4. **Resultado**: Acesso aprovado/negado
5. **Log**: Registro salvo no banco de dados

---

## 🧪 Testes

### Backend
```bash
cd agroSafe
python agroSafe/manage.py test
```

### Frontend
```bash
cd agrosafe-mvp-frontend
npm run test
```

---

## 🚀 Deploy em Produção

### Com Docker Compose
```bash
# Ajustar variáveis de ambiente no docker-compose.yml
docker-compose -f docker-compose.yml up -d
```

### Variáveis de Ambiente Necessárias

**Backend (.env)**
```
DEBUG=False
ALLOWED_HOSTS=seu-dominio.com
SECRET_KEY=sua-chave-secreta
DATABASE_URL=postgresql://user:password@host:port/db
CORS_ALLOWED_ORIGINS=https://seu-dominio.com
```

**Frontend (.env)**
```
VITE_API_URL=https://api.seu-dominio.com
VITE_APP_NAME=AgroSafe
```

---

## 📝 Migrações do Banco de Dados

O projeto utiliza migrações Django para versionamento do schema:

```bash
# Criar nova migração
python agroSafe/manage.py makemigrations

# Aplicar migrações
python agroSafe/manage.py migrate

# Ver status das migrações
python agroSafe/manage.py showmigrations
```

Migrações existentes:
- `0001_initial` - Modelo inicial
- `0002_visitante_pessoa_senha_alter_pessoa_id` - Adição de senha em Pessoa
- `0003_cadastrovisitanteportaria_registroacessoportaria` - Novos modelos
- `0005_cadastrovisitanteportaria_foto` - Campo de foto
- `0006_replace_foto_with_foto_hash` - Substituição por hash
- `0007_cadastrovisitanteportaria_empresa_nivel` - Empresa e nível
- `0008_registroacessoportaria_motivo_observacao` - Motivo e observação
- `0009_rename_pessoa_to_granja` - Renomeação de modelo
- `0010_cadastrovisitanteportaria_foto_base64` - Foto em Base64

---

## 🐛 Resolução de Problemas

### Erro de conexão entre Frontend e Backend
- Verificar se CORS está configurado corretamente
- Validar se ambos estão rodando nas portas corretas
- Checar logs com `docker-compose logs`

### Erro de reconhecimento facial
- Verificar permissão de câmera no navegador
- Garantir que a câmera funciona
- Revisar integração do OpenCV

### Erro ao migrar banco de dados
```bash
# Resetar migrações (cuidado em produção!)
python agroSafe/manage.py migrate appbk zero
python agroSafe/manage.py makemigrations
python agroSafe/manage.py migrate
```

---

## 📚 Recursos Úteis

- [Django Documentation](https://docs.djangoproject.com/)
- [Django REST Framework](https://www.django-rest-framework.org/)
- [React Documentation](https://react.dev/)
- [Vite Documentation](https://vitejs.dev/)
- [OpenCV Documentation](https://docs.opencv.org/)
- [Docker Documentation](https://docs.docker.com/)

---

## 🤝 Contribuições

Instruções para contribuir ao projeto:
1. Criar uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
2. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
3. Push para a branch (`git push origin feature/AmazingFeature`)
4. Abrir um Pull Request

---

## 📄 Licença

Distribuído sob a licença MIT. Veja `LICENSE` para mais informações.

---

## 👥 Autores

- **Equipe AgroSafe** - *Desenvolvedor Principal*

---

## 📞 Suporte

Para suporte, abra uma issue no repositório ou entre em contato com o time de desenvolvimento.

---

## ✅ Status do Projeto

- [x] Backend Django REST API
- [x] Frontend React TypeScript
- [x] Integração Frontend-Backend
- [x] Docker Compose
- [x] Sistema de Autenticação
- [x] Reconhecimento Facial (OpenCV)
- [ ] Testes automatizados completos
- [ ] Documentação de API (Swagger/OpenAPI)
- [ ] CI/CD Pipeline
- [ ] Otimizações de performance

---

**Última atualização**: Junho de 2024
