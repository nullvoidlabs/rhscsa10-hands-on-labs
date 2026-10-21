* Create the group first, then assign the user as a secondary group:

#### **Steps 1 &amp; 2: Group &amp; User Creation**

```
sudo groupadd dev-team
sudo useradd -G dev-team developer1
```

*(Note:* *\-G* *sets supplementary/secondary groups, whereas* *\-g* *sets the primary group).*

#### **Step 3: Directory Creation**

```
sudo mkdir -p /projects/internal
```

#### **Step 4: Group Ownership**

```
sudo chgrp -R dev-team /projects/internal # OR sudo chown -R :dev-team /projects/internal
```

#### **Step 5: Standard Permissions**

```
sudo chmod -R 770 /projects/internal # OR sudo chmod -R u=rwx,g=rwx,o= /projects/internal
```

#### **Step 6: Group Inheritance (Setgid)**

```
sudo chmod g+s /projects/internal
```

*(Note: In octal notation, setgid adds `2000` (`chmod 2770 /projects/internal`).*

#### **Step 7: Restricting File Deletion (Sticky Bit)**

```
sudo chmod +t /projects/internal # OR sudo chmod o+t /projects/internal
```

*(Note: In octal notation, the sticky bit adds `1000`. Combined with setgid (`2000`), the octal code for both special permissions is **3770** (`chmod 3770 /projects/internal`).*

### **Complete Ideal Exam Script**

```
# 1. Create group and user
sudo groupadd dev-team
sudo useradd -G dev-team developer1

# 2. Create directory structure
sudo mkdir -p /projects/internal

# 3. Set group ownership
sudo chgrp -R dev-team /projects/internal

# 4. Apply permissions (rwx for owner/group, none for others + Setgid + Sticky bit)
sudo chmod 3770 /projects/internal

```

