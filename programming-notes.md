
1. 生一个用纯c编写的目录遍历函数

讯飞星火
```


#include <stdio.h>
#include <dirent.h>
#include <string.h>

void traverse_directory(const char* directory) {
    DIR* dir;
    struct dirent* entry;
    
    if ((dir = opendir(directory)) == NULL) {
        printf("Error opening directory %s
", directory);
        return;
    }
    
    int count = 0;
    while ((entry = readdir(dir)) != NULL) {
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0) {
            continue;
        }
        
        count++;
        char path[1024];
        snprintf(path, sizeof(path), "%s/%s", directory, entry->d_name);
        
        if (entry->d_type & DT_DIR) {
            traverse_directory(path);
        } else {
            printf("%s/%s
", directory, entry->d_name);
        }
    }
    
    closedir(dir);
    
    printf("Found %d files and directories in %s.
", count, directory);
}

int main() {
    traverse_directory("/path/to/directory");
    
    return 0;
}



```
