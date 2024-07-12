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