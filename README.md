- 👋 Hi, I’m @Keerthanakrishnant
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Keerthanakrishnant/Keerthanakrishnant is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->


sjf:

#include <stdio.h>

typedef struct {
    int id;
    float exec_time;
} Task;

void sortTasksByExecTime(Task tasks[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (tasks[i].exec_time > tasks[j].exec_time) {
                Task temp = tasks[i];
                tasks[i] = tasks[j];
                tasks[j] = temp;
            }
        }
    }
}

int main() {
    int no_of_tasks, no_of_vms;
    printf("Enter no. of tasks: ");
    scanf("%d", &no_of_tasks);
    printf("Enter no. of VMs: ");
    scanf("%d", &no_of_vms);

    Task tasks[no_of_tasks];
    for (int i = 0; i < no_of_tasks; i++) {
        tasks[i].id = i + 1;
        printf("Enter execution time of task%d: ", i + 1);
        scanf("%f", &tasks[i].exec_time);
    }

    sortTasksByExecTime(tasks, no_of_tasks);

    float vms[no_of_vms];
    for (int i = 0; i < no_of_vms; i++) {
        vms[i] = 0;
    }

    int cur_VM = 0;
    float total_wait_time = 0;

    printf("Task\tExec Time\tWait Time\tVM\n");
    for (int i = 0; i < no_of_tasks; i++) {
        int task_id = tasks[i].id;
        float exec_time = tasks[i].exec_time;

        float wait_time = vms[cur_VM];
        printf("t%d\t%.2f\t\t%.2f\t\tVM%d\n", task_id, exec_time, wait_time, cur_VM + 1);

        total_wait_time += wait_time;
        vms[cur_VM] += exec_time;

        cur_VM = (cur_VM + 1) % no_of_vms;
    }

    printf("Average waiting time = %.2f\n", total_wait_time / no_of_vms);

    return 0;
}



fcfs:
#include <stdio.h>

int main() {
    int no_of_tasks, no_of_vms;
    printf("Enter no. of tasks: ");
    scanf("%d", &no_of_tasks);
    printf("Enter no. of VMs: ");
    scanf("%d", &no_of_vms);

    float vms[no_of_vms];
    for (int i = 0; i < no_of_vms; i++) {
        vms[i] = 0;
    }

    float exec_time;
    int cur_VM = 0;
    float total_wait_time = 0;

  
    printf("Task\tExec Time\tWait Time\tVM\n");
    for (int i = 0; i < no_of_tasks; i++) {
        printf("Enter execution time of task%d: ", i + 1);
        scanf("%f", &exec_time);

        float wait_time = vms[cur_VM];
        printf("t%d\t%.2f\t\t%.2f\t\tVM%d\n", i + 1, exec_time, wait_time, cur_VM + 1);

       
        total_wait_time += wait_time;
        vms[cur_VM] += exec_time;

        cur_VM = (cur_VM + 1) % no_of_vms;
    }

    
    printf("Average waiting time = %.2f\n", total_wait_time / no_of_vms);

    return 0;
}


min:
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    char name[10];
    int mips;
    char tasks[100][10];
    int task_count;
} VM;

int compare_VM_desc(const void *a, const void *b) {
    return ((VM*)b)->mips - ((VM*)a)->mips;
}

int compare_task_asc(const void *a, const void *b) {
    return *(int*)a - *(int*)b;
}

int main() {
    int no_of_VMs, no_of_tasks;

    printf("Enter no. of VMs : ");
    scanf("%d", &no_of_VMs);
    VM VMs[no_of_VMs];

    for (int i = 0; i < no_of_VMs; i++) {
        printf("Enter the MIPS capacity of VM%d : ", i + 1);
        scanf("%d", &VMs[i].mips);
        sprintf(VMs[i].name, "VM%d", i + 1);
        VMs[i].task_count = 0;
    }

    qsort(VMs, no_of_VMs, sizeof(VM), compare_VM_desc);

    printf("Enter no. of tasks : ");
    scanf("%d", &no_of_tasks);
    int tasks[no_of_tasks];

    for (int i = 0; i < no_of_tasks; i++) {
        printf("Enter the length of task%d : ", i + 1);
        scanf("%d", &tasks[i]);
    }

    qsort(tasks, no_of_tasks, sizeof(int), compare_task_asc);

    int vm_index = 0;
    for (int i = 0; i < no_of_tasks; i++) {
        sprintf(VMs[vm_index].tasks[VMs[vm_index].task_count], "t%d", i + 1);
        VMs[vm_index].task_count++;
        vm_index = (vm_index + 1) % no_of_VMs;
    }

    printf("--- MIN MIN ---\n");
    for (int i = 0; i < no_of_VMs; i++) {
        printf("%s -> ", VMs[i].name);
        for (int j = 0; j < VMs[i].task_count; j++) {
            printf("%s ", VMs[i].tasks[j]);
        }
        printf("\n");
    }

    return 0;
}


max:
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    char name[10];
    int mips;
    char tasks[100][10];
    int task_count;
} VM;

int compare_VM(const void *a, const void *b) {
    return ((VM*)b)->mips - ((VM*)a)->mips;
}

int compare_task(const void *a, const void *b) {
    return *(int*)b - *(int*)a;
}

int main() {
    int no_of_VMs, no_of_tasks;

    printf("Enter no. of VMs : ");
    scanf("%d", &no_of_VMs);
    VM VMs[no_of_VMs];

    for (int i = 0; i < no_of_VMs; i++) {
        printf("Enter the MIPS capacity of VM%d : ", i + 1);
        scanf("%d", &VMs[i].mips);
        sprintf(VMs[i].name, "VM%d", i + 1);
        VMs[i].task_count = 0;
    }

    qsort(VMs, no_of_VMs, sizeof(VM), compare_VM);

    printf("Enter no. of tasks : ");
    scanf("%d", &no_of_tasks);
    int tasks[no_of_tasks];

    for (int i = 0; i < no_of_tasks; i++) {
        printf("Enter the length of task%d : ", i + 1);
        scanf("%d", &tasks[i]);
    }

    qsort(tasks, no_of_tasks, sizeof(int), compare_task);

    int vm_index = 0;
    for (int i = 0; i < no_of_tasks; i++) {
        sprintf(VMs[vm_index].tasks[VMs[vm_index].task_count], "t%d", i + 1);
        VMs[vm_index].task_count++;
        vm_index = (vm_index + 1) % no_of_VMs;
    }

    printf("--- MAX MIN ---\n");
    for (int i = 0; i < no_of_VMs; i++) {
        printf("%s -> ", VMs[i].name);
        for (int j = 0; j < VMs[i].task_count; j++) {
            printf("%s ", VMs[i].tasks[j]);
        }
        printf("\n");
    }

    return 0;
}
