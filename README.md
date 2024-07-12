# JavaAirportProject

-- Active: 1714075538942@@127.0.0.1@3306@airport
create TABLE document_types(
    id int primary key auto_increment
    name varchar(40) not null
);

create table customers(
    id varchar(20) primary key AUTO_INCREMENT,
    name varchar(30) not null,
    age int not null,
    iddocument int not null,
    Foreign Key (iddocument) REFERENCES document_types(id)
);

create table trips(
    id int primary key AUTO_INCREMENT,
    trip_date date not null,
    price_trip double not null,
);
create table trip_bookings(
    id int primary key AUTO_INCREMENT,
    booking_date date not null,
    idtrip int not null,
    Foreign Key (idtrip) REFERENCES trips(id)
);
create table flight_fares(
    id int PRIMARY key AUTO_INCREMENT,
    description varchar(20) not null,
    detail text not null,
    value double(7, 3) not null
);
create table trip_booking_details(
    id int primary key AUTO_INCREMENT,
    idtrip_booking int not null,
    idcustomer int not null,
    idflight_fare int not null,
    Foreign Key (idtrip_booking) REFERENCES trip_bookings(id),
    Foreign Key (idcustomer) REFERENCES customers(id),
    Foreign Key (idflight_fare) REFERENCES flight_fares(id)
);
create table airlines(
    id int primary key AUTO_INCREMENT,
    name varchar(30) not null
);
create table tripulation_roles(
    id int primary key AUTO_INCREMENT,
    name varchar(40) not null
);
create table countries(
    id varchar(5) PRIMARY key AUTO_INCREMENT,
    name varchar(30) not null
);
create table cities(
    id varchar(5) PRIMARY key AUTO_INCREMENT,
    name varchar(30) not null,
    idcountry varchar(5) not null,
    Foreign Key (idcountry) REFERENCES countries(id)
);
create table airports(
    id varchar(5) PRIMARY KEY AUTO_INCREMENT,
    name varchar(50) not null,
    idcity varchar(5) not null,
    Foreign Key (idcity) REFERENCES cities(id)
);
create table employees(
    id int PRIMARY KEY AUTO_INCREMENT,
    name varchar(40) not null,
    ingressdate date not null,
    idrol int not null,
    idairline int not null,
    idairport varchar(5) not null,
    Foreign Key (idrol) REFERENCES tripulation_roles(id),
    Foreign Key (idairline) REFERENCES airlines(id),
    Foreign Key (idairport) REFERENCES airports(id)
);
create table gates(
    id int PRIMARY KEY not null AUTO_INCREMENT,
    gatenumber varchar(10) not null,
    idairport varchar(5) not null,
    Foreign Key (idairport) REFERENCES airports(id)
);
create table manufacturers(
    id int PRIMARY KEY AUTO_INCREMENT,
    name varchar(40) not null
);
create table models(
    id int PRIMARY KEY AUTO_INCREMENT,
    name varchar(30) not null,
    idmanufacturer int not null,
    Foreign Key (idmanufacturer) REFERENCES manufacturers(id)
);
create table statuses(
    id int PRIMARY KEY AUTO_INCREMENT,
    name varchar(30) not null
);
create table planes(
    id int PRIMARY KEY AUTO_INCREMENT,
    plates varchar(30) not null,
    capacity int not null,
    fabrication_date date not null,
    idstatus int not null,
    idmodel int not null,
    Foreign Key (idstatus) REFERENCES statuses(id),
    Foreign Key (idmodel) REFERENCES models(id)
);
create table flight_connections(
    id int not null,
    conneciton_number varchar(20) not null,
    idtrip int not null,
    idplane int not null,
    idairport int not null,
    Foreign Key (idtrip) REFERENCES trips(id),
    Foreign Key (idplane) REFERENCES planes(id),
    Foreign Key (idairport) REFERENCES airports(id)
);
create table trip_crews(
    idemployee int not null,
    idconneciton int not null,
    PRIMARY KEY(idemployee, idconnection),
    Foreign Key (idemployee) REFERENCES employees(id),
    Foreign Key (idconnection) REFERENCES flight_connections(id)
);
create Table revisions(
    id int PRIMARY KEY AUTO_INCREMENT,
    revision_date date not null,
    idplane int not null,
    Foreign Key (idplane) REFERENCES planes(id)
);
create table rev_employee(
    idrevision int not null,
    idemployee int not null,
    description text not null,
    primary KEY(idrevision, idemployee),
    Foreign Key (idrevision) REFERENCES revisions(id),
    Foreign Key (idemployee) REFERENCES employees(id)
);

