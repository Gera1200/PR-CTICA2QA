1. INSERT INTO users (username, email, password_hash, status, 
failed_attempts) 
VALUES ( 
'deaj2', 
'deaj2@demo.local', 
'$2b$12$S5VxS2iYqk2m2mM1lH3y5uWJ8o9o2mJ9cYHc5pQKQG1yQ9z9Vj7b
G', 
'ACTIVE', 
0 
) 
ON CONFLICT (username) DO NOTHING;

2. 