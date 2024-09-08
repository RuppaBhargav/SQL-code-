# SQL-code-

-- Create a table to store project information
CREATE TABLE Projects (
    project_id INT PRIMARY KEY AUTO_INCREMENT,
    project_name VARCHAR(255) NOT NULL,
    start_date DATE,
    end_date DATE,
    status VARCHAR(50)
);

-- Create a table to store team members
CREATE TABLE TeamMembers (
    member_id INT PRIMARY KEY AUTO_INCREMENT,
    member_name VARCHAR(255) NOT NULL,
    role VARCHAR(100),
    email VARCHAR(255) UNIQUE
);

-- Create a table to store tasks
CREATE TABLE Tasks (
    task_id INT PRIMARY KEY AUTO_INCREMENT,
    task_name VARCHAR(255) NOT NULL,
    assigned_to INT,
    project_id INT,
    due_date DATE,
    status VARCHAR(50),
    FOREIGN KEY (assigned_to) REFERENCES TeamMembers(member_id),
    FOREIGN KEY (project_id) REFERENCES Projects(project_id)
);

-- Insert sample data into the Projects table
INSERT INTO Projects (project_name, start_date, end_date, status)
VALUES ('Geo Mapping Project', '2024-09-01', '2024-12-01', 'In Progress');

-- Insert sample data into the TeamMembers table
INSERT INTO TeamMembers (member_name, role, email)
VALUES ('John Doe', 'Developer', 'john.doe@example.com'),
       ('Jane Smith', 'Data Analyst', 'jane.smith@example.com');

-- Insert sample data into the Tasks table
INSERT INTO Tasks (task_name, assigned_to, project_id, due_date, status)
VALUES ('Data Collection', 1, 1, '2024-09-15', 'Pending'),
       ('Data Analysis', 2, 1, '2024-09-30', 'Pending');

-- Query to view project details, team members, and tasks
SELECT 
    P.project_name,
    P.start_date,
    P.end_date,
    P.status AS project_status,
    T.task_name,
    TM.member_name,
    T.due_date,
    T.status AS task_status
FROM 
    Projects P
    JOIN Tasks T ON P.project_id = T.project_id
    JOIN TeamMembers TM ON T.assigned_to = TM.member_id;
