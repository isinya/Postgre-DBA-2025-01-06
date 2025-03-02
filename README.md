# Postgre-DBA-2025-01 Занятие #06
Настройка PostgreSQL 

Домашнее задание

развернуть виртуальную машину любым удобным способом
поставить на неё PostgreSQL 15 любым способом

# Установка PostgreSQL 15 AltLinux
apt-get install postgresql15-server postgresql15-server-devel    
/etc/init.d/postgresql initdb    
systemctl enable postgresql.service    
systemctl start postgresql.service    

# Установка PGBench
apt-get install postgresql15-contrib    


Производительность с настройками по умолчанию
pgbench  -U postgres -s 100  -c 90 -j 4 -T 15 -d postgres


number of transactions actually processed: 9110
number of failed transactions: 0 (0.000%)
latency average = 148.898 ms
initial connection time = 114.316 ms
tps = 604.439840 (without initial connection time)

# Рекомендовыанные настройки для актуальной конфигураци аппаратного обеспечения
# RAM 8 GB, CPU 4 core, SATA SSD
https://www.pgconfig.org/#/?max_connections=100&pg_version=15&environment_name=OLTP&total_ram=8&cpus=4&drive_type=SSD&arch=x86-64&os_type=linux
nano /var/lib/pgsql/data/postgresql.conf

# Memory Configuration
shared_buffers = 2GB
effective_cache_size = 6GB
work_mem = 29MB
maintenance_work_mem = 410MB

# Checkpoint Related Configuration
min_wal_size = 2GB
max_wal_size = 3GB
checkpoint_completion_target = 0.9
wal_buffers = -1

# Network Related Configuration
listen_addresses = '*'
max_connections = 100

# Storage Configuration
random_page_cost = 1.1
effective_io_concurrency = 200

# Worker Processes Configuration
max_worker_processes = 8
max_parallel_workers_per_gather = 2
max_parallel_workers = 2

number of transactions actually processed: 9118
number of failed transactions: 0 (0.000%)
latency average = 148.740 ms
initial connection time = 117.807 ms
tps = 605.081035 (without initial connection time)
