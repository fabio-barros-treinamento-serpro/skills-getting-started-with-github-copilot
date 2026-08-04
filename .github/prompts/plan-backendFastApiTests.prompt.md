## Plan: FastAPI tests in separate directory

Vou adicionar uma suíte de testes backend com `pytest` em um diretório raiz separado para cobrir o app FastAPI, preservando isolamento entre casos porque o estado de `activities` é global e mutável. Os testes vão seguir o padrão AAA (Arrange-Act-Assert) para manter cada caso legível e consistente, validando o caminho feliz e os principais erros dos endpoints de atividades sem mexer no app além do necessário para descoberta/importação.

**Steps**
1. Confirmar a configuração de descoberta de testes e, se fizer sentido, restringir a execução ao diretório de testes raiz.
2. Atualizar as dependências para incluir `pytest`.
3. Criar a estrutura nova dentro de `tests/` com um apoio compartilhado para `TestClient` e reset do estado global entre testes.
4. Implementar os testes no padrão AAA para listagem de atividades, inscrição com sucesso, inscrição duplicada, atividade inexistente, remoção com sucesso e remoção inválida.
5. Validar com `pytest` na raiz e corrigir só problemas locais de import, descoberta ou isolamento de estado que apareçam.

**Relevant files**
- `requirements.txt` — adicionar `pytest`.
- `pytest.ini` — manter o `pythonpath` e, se necessário, fixar a descoberta em `tests`.
- `src/app.py` — só tocar se a forma atual de importação atrapalhar os testes.
- Arquivos novos dentro de `tests/` — um apoio compartilhado e um arquivo principal de testes.

**Verification**
1. Rodar `pytest` na raiz do repositório.
2. Confirmar que os testes são descobertos a partir de `tests/`.
3. Verificar que o estado global não vaza entre testes.
4. Se houver falha de import, ajustar a menor configuração possível e rerodar a mesma suíte.

**Decisions**
- A cobertura vai incluir fluxo feliz e erros principais, como você pediu, organizados no padrão AAA.
- Os testes ficarão fora de `src/`, em um diretório separado no nível raiz.
- A suíte precisa ser independente da ordem de execução por causa do estado em memória.
