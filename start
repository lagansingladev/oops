#include <iostream>
#include <string>
#include <limits>

#define MAX 100

using namespace std;

class Customer {
public:
    string name;
    string address;
    string phone;
    string from_date;
    string to_date;
    float payment_advance;
    int booking_id;
};

class Room {
public:
    char type;
    char stype;
    char ac;
    int roomNumber;
    int rent;
    int status; // 0: Available, 1: Reserved
    Customer cust;

    Room addRoom(int rno);
    void searchRoom(int rno);
    void displayRoom(const Room &room) const;
};

Room rooms[MAX];
int roomCount = 0;

Room Room::addRoom(int rno) {
    Room room;
    room.roomNumber = rno;
    cout << "\nType AC/Non-AC (A/N) : ";
    cin >> room.ac;
    cout << "\nType Comfort (S/N) : ";
    cin >> room.type;
    cout << "\nType Size (B/S) : ";
    cin >> room.stype;
    cout << "\nDaily Rent : ";
    cin >> room.rent;
    room.status = 0;

    cout << "\nRoom Added Successfully!";
    return room;
}

void Room::searchRoom(int rno) {
    for (int i = 0; i < roomCount; i++) {
        if (rooms[i].roomNumber == rno) {
            cout << "Room Details\n";
            if (rooms[i].status == 1) {
                cout << "\nRoom is Reserved";
            } else {
                cout << "\nRoom is Available";
            }
            displayRoom(rooms[i]);
            return;
        }
    }
    cout << "\nRoom not found";
}

void Room::displayRoom(const Room &room) const {
    cout << "\nRoom Number: \t" << room.roomNumber;
    cout << "\nType AC/Non-AC (A/N): " << room.ac;
    cout << "\nType Comfort (S/N): " << room.type;
    cout << "\nType Size (B/S): " << room.stype;
    cout << "\nRent: " << room.rent;
}

class HotelMgnt : protected Room {
public:
    void checkIn();
    void getAvailRoom();
    void searchCustomer(const string &pname);
    void checkOut(int roomNum);
    void guestSummaryReport();
};

void HotelMgnt::guestSummaryReport() {
    if (roomCount == 0) {
        cout << "\nNo Guest in Hotel!";
        return;
    }

    for (int i = 0; i < roomCount; i++) {
        if (rooms[i].status == 1) {
            cout << "\nCustomer Name: " << rooms[i].cust.name;
            cout << "\nRoom Number: " << rooms[i].roomNumber;
            cout << "\nAddress: " << rooms[i].cust.address;
            cout << "\nPhone: " << rooms[i].cust.phone;
            cout << "\n---------------------------------------";
        }
    }
}

void HotelMgnt::checkIn() {
    int rno;
    cout << "\nEnter Room Number: ";
    cin >> rno;

    for (int i = 0; i < roomCount; i++) {
        if (rooms[i].roomNumber == rno) {
            if (rooms[i].status == 1) {
                cout << "\nRoom is already Booked";
                return;
            }

            cout << "\nEnter booking ID: ";
            cin >> rooms[i].cust.booking_id;
            cin.ignore(numeric_limits<streamsize>::max(), '\n');

            cout << "\nEnter Customer Name: ";
            getline(cin, rooms[i].cust.name);

            cout << "\nEnter Address: ";
            getline(cin, rooms[i].cust.address);

            cout << "\nEnter Phone: ";
            getline(cin, rooms[i].cust.phone);

            cout << "\nEnter From Date: ";
            getline(cin, rooms[i].cust.from_date);

            cout << "\nEnter To Date: ";
            getline(cin, rooms[i].cust.to_date);

            cout << "\nEnter Advance Payment: ";
            cin >> rooms[i].cust.payment_advance;

            rooms[i].status = 1;
            cout << "\nCustomer Checked-in Successfully.";
            return;
        }
    }
    cout << "\nRoom not found";
}

void HotelMgnt::getAvailRoom() {
    bool found = false;
    for (int i = 0; i < roomCount; i++) {
        if (rooms[i].status == 0) {
            displayRoom(rooms[i]);
            cout << "\n\nPress enter for next room";
            found = true;
        }
    }
    if (!found) {
        cout << "\nAll rooms are reserved";
    }
}

void HotelMgnt::searchCustomer(const string &pname) {
    for (int i = 0; i < roomCount; i++) {
        if (rooms[i].status == 1 && rooms[i].cust.name == pname) {
            cout << "\nCustomer Name: " << rooms[i].cust.name;
            cout << "\nRoom Number: " << rooms[i].roomNumber;
            cout << "\n\nPress enter for next record";
            return;
        }
    }
    cout << "\nPerson not found.";
}

void HotelMgnt::checkOut(int roomNum) {
    for (int i = 0; i < roomCount; i++) {
        if (rooms[i].status == 1 && rooms[i].roomNumber == roomNum) {
            int days;
            float billAmount;
            cout << "\nEnter Number of Days: ";
            cin >> days;
            billAmount = days * rooms[i].rent;

            cout << "\n\t######## CheckOut Details ########\n";
            cout << "\nCustomer Name: " << rooms[i].cust.name;
            cout << "\nRoom Number: " << rooms[i].roomNumber;
            cout << "\nAddress: " << rooms[i].cust.address;
            cout << "\nPhone: " << rooms[i].cust.phone;
            cout << "\nTotal Amount Due: " << billAmount << " /";
            cout << "\nAdvance Paid: " << rooms[i].cust.payment_advance << " /";
            cout << "\n*** Total Payable: " << billAmount - rooms[i].cust.payment_advance << " / only";

            rooms[i].status = 0;
            return;
        }
    }
    cout << "\nRoom not found";
}

void manageRooms() {
    Room room;
    int opt, rno, flag = 0;

    do {
        cout << "\n### Manage Rooms ###";
        cout << "\n1. Add Room";
        cout << "\n2. Search Room";
        cout << "\n3. Back to Main Menu";
        cout << "\n\nEnter Option: ";
        cin >> opt;

        switch (opt) {
            case 1:
                cout << "\nEnter Room Number: ";
                cin >> rno;
                flag = 0;
                for (int i = 0; i < roomCount; i++) {
                    if (rooms[i].roomNumber == rno) {
                        flag = 1;
                        break;
                    }
                }
                if (flag == 1) {
                    cout << "\nRoom Number is already present.\nPlease enter a unique number.";
                } else {
                    rooms[roomCount] = room.addRoom(rno);
                    roomCount++;
                }
                break;
            case 2:
                cout << "\nEnter Room Number: ";
                cin >> rno;
                room.searchRoom(rno);
                break;
            case 3:
                break;
            default:
                cout << "\nPlease enter a correct option.";
                break;
        }
    } while (opt != 3);
}

int main() {


    HotelMgnt hm;
    int opt = 0;
    string pname;

    do {
        cout << "\n######## Hotel Management #########";
        cout << "\n1. Manage Rooms";
        cout << "\n2. Check-In Room";
        cout << "\n3. Available Rooms";
        cout << "\n4. Search Customer";
        cout << "\n5. Check-Out Room";
        cout << "\n6. Guest Summary Report";
        cout << "\n7. Exit";
        cout << "\n\nEnter Option: ";
        cin >> opt;

        switch (opt) {
            case 1:
                manageRooms();
                break;
            case 2:
                if (roomCount == 0)
                {
                    cout << "\nRooms data is not available.\nPlease add the rooms first.";
                } 
                else 
                {
                    hm.checkIn();
                }
                break;
            case 3:
                if (roomCount == 0) 
                {
                    cout << "\nRooms data is not available.\nPlease add the rooms first.";
                } 
                else 
                {
                    hm.getAvailRoom();
                }
                break;
            case 4:
                if (roomCount == 0) 
                {
                    cout << "\nRooms are not available.\nPlease add the rooms first.";
                } 
                else 
                {
                    cout << "Enter Customer Name: ";
                    cin.ignore();
                    getline(cin, pname);
                    hm.searchCustomer(pname);
                }
                break;
            case 5:
                if (roomCount == 0) 
                {
                    cout << "\nRooms are not available.\nPlease add the rooms first.";
                } 
                else
                {
                    cout << "Enter Room Number: ";
                    cin >> opt;
                    hm.checkOut(opt);
                }
                break;
            case 6:
                hm.guestSummaryReport();
                break;
            case 7:
                cout << "\nTHANK YOU! FOR USING SOFTWARE";
                break;
            default:
                cout << "\nPlease enter a correct option.";
                break;
        }
    } while (opt != 7);

    return 0;
}
