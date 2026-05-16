Exercicios:

1)  127.0.0.1:6379> SET usuario "Carlos"
    OK
    127.0.0.1:6379> GET usuario
    "Carlos"
    127.0.0.1:6379> SET usuario "Carlos Silva"
    OK

2)
    127.0.0.1:6379> MSET produto "Notebook" preco "3500" estoque "15"
    OK
    127.0.0.1:6379> MGET produto preco estoque
    1) "Notebook"
    2) "3500"
    3) "15"

3)  
    127.0.0.1:6379> SETNX admin me
    (integer) 1
    127.0.0.1:6379> SETNX admin other
    (integer) 0
    127.0.0.1:6379> GET admin
    "me"
    127.0.0.1:6379> 

4)  127.0.0.1:6379> SET nome "Maria"
    OK
    127.0.0.1:6379>  SET nome "Maria Oliveira"
    OK
    127.0.0.1:6379> STRLEN nome
    (integer) 14
    127.0.0.1:6379> GETRANGE nome 0 5
    "Maria "

5)  127.0.0.1:6379> SET cidade "Campinas" 
    OK
    127.0.0.1:6379> SETRANGE cidade 0 "São "
    (integer) 8
    127.0.0.1:6379> GET cidade
    "S\xc3\xa3o nas"
1   27.0.0.1:6379> 

    --------- /* Para a correção do texto */ ------------
    (main) $ docker compose exec redis redis-cli --raw
    127.0.0.1:6379> GET cidade
    Campinas
    127.0.0.1:6379> SETRANGE cidade 0 "São "
    8
    127.0.0.1:6379> GET cidade
    São nas

6)  127.0.0.1:6379> SET pontos 10
    OK
    127.0.0.1:6379> INCRBY pontos 1
    11
    127.0.0.1:6379> INCRBY pontos 5
    16
    127.0.0.1:6379> DECRBY pontos 3
    13
    127.0.0.1:6379> GET pontos
    13

7)  127.0.0.1:6379> SET saldo 100.500
    OK
    127.0.0.1:6379> INCRBYFLOAT saldo 25.75
    126.25
    127.0.0.1:6379> GET saldo
    126.25

8)  SET token "AH22"
    127.0.0.1:6379> EXPIRE token 60
    1
    127.0.0.1:6379> TTL token
    53
    127.0.0.1:6379> PERSIST token
    (integer) 1

9)  SET sessao 1
    127.0.0.1:6379> PEXPIRE sessao 5000
    (integer) 1
    127.0.0.1:6379> TTL sessao
    (integer) 3

    10) 127.0.0.1:6379> SET curso "Redis"
    OK
    127.0.0.1:6379> RENAME curso disciplina
    OK
    127.0.0.1:6379> COPY disciplina backup_disciplina
    (integer) 1
    127.0.0.1:6379> GET backup_disciplina
    "Redis"
    127.0.0.1:6379> TYPE disciplina
    string
    127.0.0.1:6379> TYPE backup_disciplina
    string
    127.0.0.1:6379> EXISTS disciplina
    (integer) 1
    127.0.0.1:6379> DEL disciplina
    (integer) 1

11) 127.0.0.1:6379> SET atividade "Correr"
    OK
    127.0.0.1:6379> MOVE atividade 1
    (integer) 1

12) 127.0.0.1:6379> MSET carro "Opala" consulta "20/4/2026"     materia "ML" fruta "Pera" livro "Bioinformatica"
    OK

13) 127.0.0.1:6379> SCAN 0
    1) "25"
    2)  1) "consulta"
        2) "produto"
        3) "usuario"
        4) "materia"
        5) "nome"
        6) "admin"
        7) "backup_disciplina"
        8) "livro"
        9) "preco"
        10) "estoque"
        11) "token"
    127.0.0.1:6379> SCAN 25
        1) "0"
        2) 1) "fruta"
        2) "cidade"
        3) "carro"
        4) "pontos"
        5) "saldo"

13) 127.0.0.1:6379> RPUSH tarefas "Estudar Redis" "Fazer        exercicios" "Dormir"
    (integer) 3
    127.0.0.1:6379> LRANGE tarefas 0 -1
    1) "Estudar Redis"
    2) "Fazer exercicios"
    3) "Dormir"

14) 127.0.0.1:6379> LLEN  tarefas
    (integer) 3
    127.0.0.1:6379
    127.0.0.1:6379> LINDEX tarefas 0
    "Estudar Redis"
    127.0.0.1:6379> LINDEX tarefas -1
    "Dormir"

15) 127.0.0.1:6379> LSET tarefas -1 "Escovar os dentes"
    OK
    127.0.0.1:6379> LRANGE
    tarefas 0 -1
    1) "Estudar Redis"
    2) "Fazer exercicios"
    3) "Escovar os dentes"

16) 127.0.0.1:6379> LINSERT tarefas BEFORE "Escovar os dentes" "Tomar Café"
    (integer) 4
    127.0.0.1:6379> LRANGE tarefas 0 -1
    1) "Estudar Redis"
    2) "Fazer exercicios"
    3) "Tomar Caf\xc3\xa9"
    4) "Escovar os dentes"

---/ Corrigindo a desformatação ---/

@Igor-RR ➜ /workspaces/teste-redis2 (main) $ docker compose exec -it redis redis-cli --raw
127.0.0.1:6379> LRANGE tarefas 0 -1
Estudar Redis
Fazer exercicios
Tomar Café
Escovar os dentes

17) 127.0.0.1:6379> LPOP tarefas
    Estudar Redis
    127.0.0.1:6379> RPOP tarefas
    Escovar os dentes
    127.0.0.1:6379> LRANGE tarefas 0 -1
    Fazer exercicios
    Tomar Café

18) 127.0.0.1:6379> LPUSH fila_atividade_pendente "Caminhar"
    1
    127.0.0.1:6379> LPUSH fila_atividade_processando "Dados biometricos"
    1
    127.0.0.1:6379> LMOVE fila_atividade_pendente fila_atividade_processando LEFT LEFT
    Caminhar
    127.0.0.1:6379> LRANGE fila_atividade_pendente 0 -1

    127.0.0.1:6379> LRANGE fila_atividade_processando 0 -1
    Caminhar
    Dados biometricos

19) 127.0.0.1:6379> RPUSH logs "LSET" "LPOP" "RPOP" "LINDEX" "LRANGE" "LLEN" "RPUSH" "LPUSH" "LMOVE" "LINSERT"
    10
    127.0.0.1:6379> LTRIM logs 5 -1
    OK
    127.0.0.1:6379> LRANGE logs 0 -1
    LLEN
    RPUSH
    LPUSH
    LMOVE
    LINSERT

20) 127.0.0.1:6379> LRANGE tarefas 0 -1
    Fazer exercicios
    Tomar Café
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    3
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    4
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    5
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    6
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    7
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    8
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    9
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    10
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    11
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    12
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    13
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    14
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    15
    127.0.0.1:6379> LPUSH tarefas "Dormir"
    127.0.0.1:6379> LREM tarefas 1 "Dormir"
    1
    127.0.0.1:6379> LREM tarefas 0 "Dormir"
    13

21) 127.0.0.1:6379> LPOS        tarefas "Estudar Redis"

(OBS: Estudar redis foi excluido em uma das operações)

127.0.0.1:6379> LPUSH tarefas "Estudar Redis"
3
127.0.0.1:6379> RPUSH tarefas "Estudar Redis"
4
127.0.0.1:6379> LPOS tarefas "Estudar Redis" COUNT 0
0
3

22) 127.0.0.1:6379> LPOP tarefas 2
Estudar Redis

23) 127.0.0.1:6379> EXPIRE tarefas 60
    1
    127.0.0.1:6379> TTL tarefas
    51
    127.0.0.1:6379> EXISTS tarefas
    0











    





    
