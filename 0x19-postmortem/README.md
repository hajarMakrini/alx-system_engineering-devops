# Postmortem: Memory Leak in Application
![img](alx-system_engineering-devops/0x19-postmortem
/Screenshot 2024-06-22 at 22-34-59 image illustre Memory Leak in Application - Recherche Google.png)

## Issue Summary

- **Duration of the outage:** June 18, 2024, 09:00 to 11:45 UTC
- **Impact:** The main web application experienced significant slowdowns and crashes. Approximately 75% of users were affected, leading to a poor user experience and an inability to access the service.
- **Root cause:** Memory leak in the recent update of the application server software.

## Timeline

- **09:00 UTC:** Issue detected via monitoring alert indicating high memory usage on the application servers.
- **09:05 UTC:** On-call engineer received the alert and began investigating.
- **09:15 UTC:** Initial assumption was increased traffic; load balancer logs checked but traffic was normal.
- **09:30 UTC:** Error logs showed repeated "Out of Memory" exceptions on several servers.
- **09:45 UTC:** Misleading path taken by restarting affected servers, temporarily alleviating the issue but not resolving the root cause.
- **10:00 UTC:** Escalated to the development team for further investigation.
- **10:30 UTC:** Development team identified a memory leak introduced in the latest update.
- **11:00 UTC:** Rollback of the latest update began.
- **11:30 UTC:** Rollback completed; memory usage returned to normal levels.
- **11:45 UTC:** Confirmed all systems operational and monitored for an additional hour to ensure stability.

## Root Cause and Resolution

- **Root Cause:** The root cause of the outage was a memory leak in the recent update of the application server software. A specific function within the new feature was not properly releasing memory after use, causing memory usage to increase continuously until the servers ran out of memory and crashed.
- **Resolution:** The issue was resolved by rolling back the application to the previous stable version. The development team then identified and fixed the memory leak in the problematic function. Additional testing was conducted to ensure the fix was effective.

## Corrective and Preventative Measures

**Improvements:**
- Enhance code review processes to include checks for memory management.
- Implement more comprehensive performance and memory usage testing before deploying updates.
- Improve monitoring to detect memory leaks earlier.

**Tasks:**
- **Update Deployment Process:** Revise the deployment checklist to include memory management checks and load testing.
- **Enhance Monitoring:** Implement detailed monitoring of memory usage for all application servers.
- **Improve Logging:** Enhance logging to capture detailed memory allocation and deallocation information.
- **Conduct Training:** Provide training for the development team on best practices for memory management and leak detection.
- **Documentation Update:** Update internal documentation to include procedures for handling memory-related issues and steps for quick resolution.

---

**Directed by:** Hajar Makrini

