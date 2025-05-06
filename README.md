# week8d
-- Use or create database
CREATE DATABASE IF NOT EXISTS LibraryDB;
USE LibraryDB;

-- 1. Members Table
CREATE TABLE Members (
    MemberID INT PRIMARY KEY AUTO_INCREMENT,
    FullName VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    JoinDate DATE NOT NULL
);

-- 2. Authors Table
CREATE TABLE Authors (
    AuthorID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(100) NOT NULL
);

-- 3. Books Table
CREATE TABLE Books (
    BookID INT PRIMARY KEY AUTO_INCREMENT,
    Title VARCHAR(150) NOT NULL,
    ISBN VARCHAR(20) UNIQUE NOT NULL,
    PublishedYear YEAR,
    CopiesAvailable INT DEFAULT 0
);

-- 4. BookAuthors Table (Many-to-Many between Books and Authors)
CREATE TABLE BookAuthors (
    BookID INT,
    AuthorID INT,
    PRIMARY KEY (BookID, AuthorID),
    FOREIGN KEY (BookID) REFERENCES Books(BookID),
    FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID)
);

-- 5. BorrowRecords Table
CREATE TABLE BorrowRecords (
    RecordID INT PRIMARY KEY AUTO_INCREMENT,
    MemberID INT,
    BookID INT,
    BorrowDate DATE NOT NULL,
    ReturnDate DATE,
    FOREIGN KEY (MemberID) REFERENCES Members(MemberID),
    FOREIGN KEY (BookID) REFERENCES Books(BookID)
);

-- Sample Data

-- Members
INSERT INTO Members (FullName, Email, JoinDate) VALUES
('John Doe', 'john@example.com', '2023-01-10'),
('Jane Smith', 'jane@example.com', '2023-02-15');

-- Authors
INSERT INTO Authors (Name) VALUES
('George Orwell'),
('J.K. Rowling');

-- Books
INSERT INTO Books (Title, ISBN, PublishedYear, CopiesAvailable) VALUES
('1984', '9780451524935', 1949, 5),
('Harry Potter and the Sorcerer\'s Stone', '9780439708180', 1997, 3);

-- BookAuthors (linking books and authors)
INSERT INTO BookAuthors (BookID, AuthorID) VALUES
(1, 1), -- 1984 by George Orwell
(2, 2); -- Harry Potter by J.K. Rowling

-- BorrowRecords
INSERT INTO BorrowRecords (MemberID, BookID, BorrowDate, ReturnDate) VALUES
(1, 1, '2024-03-01', '2024-03-15'),
(2, 2, '2024-03-05', NULL);
