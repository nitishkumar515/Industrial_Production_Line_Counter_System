# Industrial_Production_Line_Counter_System
## Introduction 

In this project, I aim to Design and build a Production Line Counter System  using smart sensor to fully embrace automation. The method uses Industrial Automation systems and smart sensors to maintain and bring the accuracy over counting. This methodology can be implemented in any Industry. This method is cost efficient and can be easily implemented. I am implementing this all on riscv processor rather than arduino board.

## Advantages
1. The Number Counting System brings more accuracy over counting.
2. More efficient.
3. Cost implementation is less.
4. Reduces man power over the industries.
5. Automated Tireless counting.
6. No Error probability in counting.
7. Keep Count Data Stored as well as Display live count.

## Uses
1. Detecting objects on the roller conveyer.
2. Detecting cartons on the conveyer.
3. Counting screws.
4. Detecting engine block on the conveyer.
5. Detecting body in the coating process.
6. Detecting PC board.
7. Counting wafers.
8. Detecting pizza dough.
## Requirements

Here I am using *Z3R-400* Standard retro-reflective sensor. The small beam of the Z3R-400 sensor allows for detecting or counting product flowing through a a process with narrow spaces. The sensor can detect the interruption to a reflected light beam, and decide if an object is present or not.
### Sensor

![sensor](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/59d67f88-47c2-4b5f-8a49-51082f456121)


## Block Diagram
![blo](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/8e505ea4-a3b2-4001-a0fc-fe4a352251a0)


## C Code
```
#include <stdio.h>

int count = 0;

void increment_Count()
{
 count =count + 1;
  printf("Item produced. Current count: %d\n", count);
 }

void decrement_Count()
 {
    if (count > 0)
 {
        count = count - 1;
        printf("Item removed. Current count: %d\n", count);
    }
else
{
        printf("No items to remove. Current count is zero.\n");
    }
}

void displayCount()
{
    printf("Current count: %d\n", count);
}

int main()
 {
    bool running = 1;
    int choice;

    while (running)
 {
        printf("\nProduction Line Counter System\n");
        printf("1. Produce an item\n");
        printf("2. Remove an item\n");
        printf("3. Display current count\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
{
            case 1:
                incrementCount();
                break;
            case 2:
                decrementCount();
                break;
            case 3:
                displayCount();
                break;
            case 4:
                running = 0;
                break;
            default:
                printf("Invalid choice. Please try again.\n");
                break;
        }
    }

    printf("Exiting the system.\n");
    return 0;
}
```

![Screenshot from 2023-10-05 23-16-45](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/f211635c-a9c4-47ac-9d27-cb411ee5506a)




