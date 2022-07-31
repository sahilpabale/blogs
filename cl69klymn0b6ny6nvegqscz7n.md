## Introducing Grassp: Micro-Learning made more fun for CLIs 👀

# What is Grassp? 👨🏻‍💻
[Grassp](https://www.npmjs.com/package/grassp) is the first Open-Source CLI-based Micro-Learning service that caters to all extensive terminal users. The aim was to make learning more accessible by porting it into the terminals themselves so that everything is a few commands away.

# Inspiration ✨
As a backend and CLI dev, I knew about the immense potential of TUIs and CLIs. But their use cases were really specific and were rarely used. The learning lifecycle of a developer is never ending, he keeps on learning new things every day. But the main medium of interaction for learning is only browsers. 

Then the thought struck my mind as to why shouldn't I make a micro-learning CLI-based tool for developers. It would not only popularize TUIs and CLIs and make them mainstream but also make learning quick and accessible.

That marked the start of my journey in building Grassp. The idea was not to make a full-fledged learning platform in the terminal, but something that introduces concise learning to developers in the terminal. The reason behind so is that content distribution is very new in terminals and requires further development, and Grassp marks the start of it.

# How I built Grassp 🏗
The real challenge was to find proper libraries to construct the TUI for this. Initially, I had lots of plans to build a dashboard and add interactivity to it. But later realized that the Node.js ecosystem doesn't have enough supporting libraries that go hand in hand. 

As I recall, I have used 4 to 5 terminal libraries. None synced with [Oclif](https://oclif.io/) - the core CLI building library. Then I came through an article where I got to know I can even use React in CLI 🤯 All my friends were in awe by listening to this.

Then there's this library - React Ink which helped me render some components on TUI. I also explored ink, blessed, neo-blessed, and many more but the problem was they couldn't sync well with each other.

# Application Flow 🚀

![App Flow Diagram](https://cdn.hashnode.com/res/hashnode/image/upload/v1659275117579/QHCVVFLpF.png align="left")

This application flow consists of many elements (CLI client, Proxy API Server, and PlanetScale DB)

The CLI doesn't directly interact with the Planetscale database. The request first goes to a Proxy API which then acts accordingly.

The `access_token` is a hidden file containing the logged-in user's token, which gets passed to the API on every request.

The API then verifies the token, if it's authorized to access the data. If true, then the user can perform actions, or else he might need to log in again to use the app!

## Install the CLI 💿

- To use [Grassp CLI](https://www.npmjs.com/package/grassp) , you need [Node.js](https://nodejs.org)  installed on your computer!

- After installing Node.js, verify if it works fine using `$ node --version` and check if it returns a specific version. Then you're good to go!

- Now use this command to install Grassp through **npm** - `$ npm install -g grassp` (You can also use Yarn and PNPM to install)

- After installing it globally, just run this command `$ grassp` to confirm if grassp is installed or not

![grassp cli](https://cdn.hashnode.com/res/hashnode/image/upload/v1659276069032/YynEiGuEG.png align="left")

### Woohoo, the CLI is installed 🎉 🎉

<hr/>

## Let's explore the CLI✨

- There are total 6 main commands and 1 help command which you can use and play with :D

### `$ grassp signup`
The first time you use grassp, you need to use the `signup` command to create your account.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659276321958/aCOJex2xH.png align="left")

You'll get a confirmation link at your provided email address. Click on it to get started!

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659276494018/XCEZUU-v4.png align="center")

### `$ grassp login`
After verifying your email address you can now log in using the `login` command.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659276611922/T_4n2hpmU.png align="left")

### `$ grassp whoami`
Whoami is a universal command to know more about the logged-in user.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659286713777/d_EveeUHq.png align="left")

### `$ grassp update interests`
If you ever need to update your interests, this command is at your service!

### `$ grassp learn`
The main command to quickly learn new topics directly in the CLI!

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659277871167/A-Ul2hSb8.png align="left")

There are several modules based on the Interest you select. And every module has micro cards embedded in it.

### `$ grassp logout`
Finally, if you wish to log out, use this command. It will also revoke your token👋👋

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659286829655/cxXaCXCwy.png align="left")
<hr/>

## Tech Stack 👨‍💻

1. **TypeScript**
2. **Node.js** - the environment for CLI and API
3. **Express.ts API** - to build the Proxy API
4. **PlanetScale DB** - primary database used to store data
5. **Oclif, Inquirer and React Ink** - for creating the interactive CLI
7. **Fly.io** - for deploying the Proxy API
8. **Npm.js**  - to publish and distribute the CLI

## Schema of Database

```
model Users {
  id              String               @id @default(uuid())
  email           String               @unique @db.VarChar(255)
  password        String
  fullName        String               @db.VarChar(255)
  isVerified      Boolean              @default(false)
  interests       Interests[]          @relation("UsersInterests")
  modulesProgress UserModuleProgress[]
  createdAt       DateTime             @default(now())
  updatedAt       DateTime             @updatedAt
}

model Interests {
  id        String    @id @default(uuid())
  name      String    @unique
  title     String
  users     Users[]   @relation("UsersInterests")
  createdAt DateTime  @default(now())
  updatedAt DateTime  @updatedAt
  modules   Modules[]
}

model Modules {
  id            String               @id @default(uuid())
  title         String               @db.VarChar(255)
  difficulty    Difficulty
  cards         Cards[]
  usersProgress UserModuleProgress[]
  createdAt     DateTime             @default(now())
  updatedAt     DateTime             @updatedAt
  interest      Interests            @relation(fields: [interestId], references: [name])
  interestId    String
}

model Cards {
  id        String   @id @default(uuid())
  moduleId  String
  module    Modules  @relation(fields: [moduleId], references: [id])
  title     String   @db.VarChar(255)
  content   String   @db.Text
  order     Int
  link      String?  @db.Text
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model UserModuleProgress {
  user       Users    @relation(fields: [userId], references: [id])
  userId     String
  module     Modules  @relation(fields: [moduleId], references: [id])
  moduleId   String
  isFinished Boolean  @default(false)
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt

  @@id([userId, moduleId])
}

enum Difficulty {
  Beginner
  Intermediate
  Advanced
}
```

# Deployement

I used this amazing service called fly.io, to not only host and deploy the API but also free of cost! 🤯

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659279237269/P9vY4MIdR.png align="left")

# Future Developments

- As mentioned earlier, this CLI is just scratching the surface of a large-scale CLI adoption and requires many improvements and developments in order to make the UX more simpler and friendly.
- Hence after this hackathon, I would primarily be working on adding more TUI (Terminal UI) components that enrich user interaction which is another massive step towards improving CLI usage and building a better ecosystem overall along with growth in quality content and accessibility

# Source Code 👨‍💻

- #### Grassp CLI Repo - https://github.com/sahilpabale/grassp
- #### Grassp API Repo - https://github.com/sahilpabale/grassp-api
- #### NPM Package - https://npmjs.com/package/grassp

If you find any bugs or problems, feel free to create an issue or fork the repo to contribute 😄😄

# Connect with me 👋🏻

- [Twitter](https://twitter.com/SahilPabale)
- [LinkedIn](https://www.linkedin.com/in/sahil-pabale/)
- Discord (sahilpabale#8371)
- Email at dev.sahilpabale@gmail.com

Do add your thoughts or if you have any questions to ask, drop them below in the comments. Have a great day ❤️
