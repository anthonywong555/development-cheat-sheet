# Cookies vs. Local Storage vs. Session Storage

This table was taken from [Web Dev Simplified](https://youtu.be/GihQAC1I39Q?si=Qk7T414yc9PXWblT)

|                         | **Cookies**        | **Local Storage** | **Session Storage** |
|-------------------------|--------------------|-------------------|---------------------|
| **Capacity**             | 4kb                | 10mb              | 5mb                 |
| **Browsers**             | HTML4 / HTML 5     | HTML 5            | HTML 5              |
| **Accessible from**      | Any window         | Any window        | Same tab            |
| **Expires**              | Manually set       | Never             | On tab close        |
| **Storage Location**     | Browser and server | Browser only      | Browser only        |
| **Sent with requests**   | Yes                | No                | No                  |
| **Examples**             | Authentication, user preferences | Caching, persistent data | Session-based data (e.g., form data) |
| **Reference**   |                 | [Link](https://rodneylab.com/using-local-storage-sveltekit/)                |                   |