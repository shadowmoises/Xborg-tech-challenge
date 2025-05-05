# Xborg-tech-challenge
MY attempt at the Xborg tech challenge

Hello all,
 
This was my effort at attempting to complete the Xborg tech challenge.
TL:DR - I didn't, my experience is more in functional QA and this task whooped me. Below are notes explaining my efforts in getting my machine setup in order to attempt the task, which I couldn't. The notes start at the point I installed docker on my machine and it was crashing upon launch. All actions explained in the bottom were performed on the VScode terminal, except for enabling SVM in my machine BIOS and one instance where I used Powershell in admin mode

Thank you for the opportunity, despite the end result, I did have fun learning how to setup the different tools on my machine.

 Moe
====================================================================================
Tools installed through the process:

**Node.Js
**VSCode with extensions
- Dev Containers
- Nest Essentials
- Pratics NestJS snippets for VS code
- WSL
- Docker
- ESLint
- Live Preview
- Monorepo Workspace
- Prettier
- SQLite
**Docker Desktop
**ChatGPT for troubleshooting
(Attempted to troubleshoot using basic google search but wasn't as helpful)
**Ubuntu
**WSL (desktop shell)

Tools also used:

-CMD prompt
-Powershell
===================================================================================

Errors with setup and fixes:

Docker containers:

- Installed docker extension on VScode
-- VScode would report that docker wasn't installed
--- First attempted to uninstall/reinstall extension on VScode
** Still reported as not installed

- Installed Docker on my desktop
-- Upon launching Docker displayed -Unexpected WSL error

"deploying WSL2 distributions
ensuring main distro is deployed: deploying "docker-desktop": importing WSL distro "WSL2 is not supported with your current machine configuration.\r\nPlease enable the \"Virtual Machine Platform\" optional component and ensure virtualization is enabled in the BIOS.\r\nEnable \"Virtual Machine Platform\" by running: wsl.exe --install --no-distribution\r\nFor information please visit https://aka.ms/enablevirtualization\r\nError code: Wsl/Service/RegisterDistro/CreateVm/HCS/HCS_E_HYPERV_NOT_INSTALLED\r\n" output="docker-desktop": exit code: 4294967295: running WSL command wsl.exe C:\Windows\System32\wsl.exe --import docker-desktop <HOME>\AppData\Local\Docker\wsl\main C:\Program Files\Docker\Docker\resources\wsl\wsl-bootstrap.tar --version 2: WSL2 is not supported with your current machine configuration.
Please enable the "Virtual Machine Platform" optional component and ensure virtualization is enabled in the BIOS.
Enable "Virtual Machine Platform" by running: wsl.exe --install --no-distribution
For information please visit https://aka.ms/enablevirtualization
Error code: Wsl/Service/RegisterDistro/CreateVm/HCS/HCS_E_HYPERV_NOT_INSTALLED
: exit status 0xffffffff
checking if isocache exists: CreateFile \\wsl$\docker-desktop-data\isocache\: The network name cannot be found."

*** enabled SVM setting in my bios (due to having an AMD setup) Docker initialized upon restart.

- figuring out how to deploy/run the app in the tech test.
-- bash is not supported by VScode naturally, learned that the hard way by attempting it on cmd prompt and powershell.
--- installed the WSL extension on VScode
--- continued to have issues as I didn't actually install wsl only the extension
--- execute command wsl --install
*** wsl installed on my machine
** executed command wsl.exe -d Ubuntu
*** provisioned new WSL instance

-Attempted to run bash could not
-- Executed sudo bash
** bash could then be performed

- Attempted to execute yarn command
-- Could not
--- executed command 'corepack enable' then corepack prepare yarn@stable --activate
*** performed yarn --version system returned : 0.32+git

- Attempting to launch the infrastructure led to other issues.
-- On VSCode selected the package.json from client folder within apps
--- initiated the Debug function then selected Start:next start | which auto performed 'npm run start'
** Terminal displayed error " File C:\Program Files\nodejs\npm.ps1 cannot be loaded because running scripts is disabled on this system.........."

 - Launched a stand alone instance of Powershell in Admin mode
 -- Performed command: Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
 ** able to perform Debug function on selected package.json (apps\client) 
 *** Produced errors: 
 'next' is not recognized as an internal or external command,
operable program or batch file.
npm error Lifecycle script `start` failed with error:
npm error code 1
npm error path C:\Users\kornb\OneDrive\Desktop\Xborg Tech Test\QA_Engineer_Challenge\xborg-backend-challenge-main\apps\client
npm error workspace client@0.0.0
npm error location C:\Users\kornb\OneDrive\Desktop\Xborg Tech Test\QA_Engineer_Challenge\xborg-backend-challenge-main\apps\client
npm error command failed
npm error command C:\Windows\system32\cmd.exe /d /s /c next start
 
- Attempt to execute debug function Start: nest start | Start: next Start | build: turbo run build :  on package.json located in the main folder.
** All produced similar error to above stating "nest", "next" and "build" were not recognized

- executed npm install -g @nestjs/cli
** added 248 packages in 11s

45 packages are looking for funding
  run `npm fund` for details
- executed nest --version
** 11.0.7

- executed npx next dev
** prompted to install next@15.3.1 [Confirmed with 'Y']
***    ▲ Next.js 15.3.1
   - Local:        http://localhost:3000
   - Network:      http://172.31.128.1:3000

 ✓ Starting...
Attention: Next.js now collects completely anonymous telemetry regarding usage.
This information is used to shape Next.js' roadmap and prioritize features.
You can learn more, including how to opt-out if you'd not like to participate in this anonymous program, by visiting the following URL:
https://nextjs.org/telemetry

[Error: > Couldn't find any `pages` or `app` directory. Please create one under the project root]
-- executed ls next
** xborg-tech-challenge@ C:\Users\kornb\OneDrive\Desktop\Xborg Tech Test\QA_Engineer_Challenge\xborg-backend-challenge-main
└── (empty)

-- attempted to execute: yarn list next
** Error: ".....'yarn' is not recognized
- executed: npm install -g yarn
** added 1 package in 1s
- yarn --version
** 1.22.22
-- reattempted :  yarn list next
** yarn list v1.22.22
warning Filtering by arguments is deprecated. Please use the pattern option instead.
└─ next@13.4.5

- With package.json selected from main folder, executed: yarn docker compose --file .local/docker-compose.yml up --detach
** yarn run v1.22.22
error Command "docker" not found.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
-- docker --version
*** Docker version 28.1.1, build 4eba377

- Restarted machine relaunched Docker and VScode
-- Prompted to install Dev Containers -> installed Dev Containers
-- Add main folder to Dev Containers in "node.js & Typescript" configuration
--- Selected 22-bookworm for node.js version
---- selected for install: Bash automated testing system, Bash command, Bash profile, corepack (via npm), NestJS CLI (via npm), Node.js (nvm), nx (via npm), SQLite, TypeScript (Global), Turborepo (via npm), Yarn - presistent cache.
** After confirming options, nothing seemed to occur.
-- Repeated process of opening Main Folder in Dev Container, process initialized and opened a new Dev Container, appeared to install all options selected during the first attempt.
** Running the onCreateCommand from Feature 'ghcr.io/nikobockerman/devcontainer-features/yarn-persistent-cache:1'...

[119740 ms] Start: Run in container: /usr/local/share/github-nikobockerman/devcontainer-features/yarn-persistent-cache/onCreate.sh
Done. Press any key to close the terminal.
***New VScode instance opened in a DEV container

- In new VScode instance with Dev Container initialized, opened package.json from main folder with Terminal
** node ➜ /workspaces/xborg-backend-challenge-main $
-- executed : yarn start docker compose --file .local/docker-compose.yml up --detach
** yarn run v1.22.22
error Command "start" not found.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.

- Clicked over to the package.json in the api folder inside apps
-- performed action Debug -> Start : nest start 
**** node ➜ /workspaces/xborg-backend-challenge-main/apps/api $ yarn run start
Debugger attached.
yarn run v1.22.22
$ nest start
Debugger attached.
error TS2468: Cannot find global value 'Promise'.
src/app.module.ts:1:24 - error TS2307: Cannot find module '@nestjs/common' or its corresponding type declarations.

1 import { Module } from '@nestjs/common';
                         ~~~~~~~~~~~~~~~~
src/app.module.ts:2:30 - error TS2307: Cannot find module '@nestjs/config' or its corresponding type declarations.

2 import { ConfigModule } from '@nestjs/config';
                               ~~~~~~~~~~~~~~~~
src/config/env/env-config.ts:10:11 - error TS2580: Cannot find name 'process'. Do you need to install type definitions for node? Try `npm i --save-dev @types/node`.

10   switch (process.env.NODE_ENV) {
             ~~~~~~~
src/config/env/production.ts:2:17 - error TS2580: Cannot find name 'process'. Do you need to install type definitions for node? Try `npm i --save-dev @types/node`.

2   DATABASE_URL: process.env.DATABASE_URL,
                  ~~~~~~~
src/config/env/production.ts:5:13 - error TS2580: Cannot find name 'process'. Do you need to install type definitions for node? Try `npm i --save-dev @types/node`.

5     SECRET: process.env.JWT_SECRET,
              ~~~~~~~
src/main.ts:1:35 - error TS2307: Cannot find module '@nestjs/common' or its corresponding type declarations.

1 import { INestMicroservice } from '@nestjs/common';
                                    ~~~~~~~~~~~~~~~~
src/main.ts:2:29 - error TS2307: Cannot find module '@nestjs/core' or its corresponding type declarations.

2 import { NestFactory } from '@nestjs/core';
                              ~~~~~~~~~~~~~~
src/main.ts:3:48 - error TS2307: Cannot find module '@nestjs/microservices' or its corresponding type declarations.

3 import { MicroserviceOptions, Transport } from '@nestjs/microservices';
                                                 ~~~~~~~~~~~~~~~~~~~~~~~
src/main.ts:8:16 - error TS2705: An async function or method in ES5 requires the 'Promise' constructor.  Make sure you have a declaration for the 'Promise' constructor or include 'ES2015' in your '--lib' option.

8 async function bootstrap() {
                 ~~~~~~~~~
src/prisma/prisma.module.ts:1:32 - error TS2307: Cannot find module '@nestjs/common' or its corresponding type declarations.

1 import { Global, Module } from '@nestjs/common';
                                 ~~~~~~~~~~~~~~~~
src/prisma/prisma.service.ts:6:8 - error TS2307: Cannot find module '@nestjs/common' or its corresponding type declarations.

6 } from '@nestjs/common';
         ~~~~~~~~~~~~~~~~
src/prisma/prisma.service.ts:7:31 - error TS2307: Cannot find module '@nestjs/config' or its corresponding type declarations.

7 import { ConfigService } from '@nestjs/config';
                                ~~~~~~~~~~~~~~~~
src/prisma/prisma.service.ts:8:30 - error TS2307: Cannot find module '@prisma/client' or its corresponding type declarations.

8 import { PrismaClient } from '@prisma/client';
                               ~~~~~~~~~~~~~~~~
src/prisma/prisma.service.ts:12:54 - error TS2339: Property 'name' does not exist on type 'typeof PrismaService'.

12   private readonly logger = new Logger(PrismaService.name);
                                                        ~~~~
src/prisma/prisma.service.ts:29:16 - error TS2339: Property '$connect' does not exist on type 'PrismaService'.

29     await this.$connect();
                  ~~~~~~~~
src/prisma/prisma.service.ts:35:10 - error TS2339: Property '$on' does not exist on type 'PrismaService'.

35     this.$on('beforeExit', async () => {
            ~~~
src/prisma/prisma.service.ts:35:28 - error TS2705: An async function or method in ES5 requires the 'Promise' constructor.  Make sure you have a declaration for the 'Promise' constructor or include 'ES2015' in your '--lib' option.

35     this.$on('beforeExit', async () => {
                              ~~~~~~~~~~~~~
src/prisma/types/user.types.ts:1:24 - error TS2307: Cannot find module '@prisma/client' or its corresponding type declarations.

1 import { Prisma } from '@prisma/client';
                         ~~~~~~~~~~~~~~~~
src/user/__tests__/mocks.ts:1:27 - error TS2307: Cannot find module 'lib-server' or its corresponding type declarations.

1 import { SignUpDTO } from 'lib-server';
                            ~~~~~~~~~~~~
src/user/user.controller.ts:1:36 - error TS2307: Cannot find module '@nestjs/common' or its corresponding type declarations.

1 import { Controller, Logger } from '@nestjs/common';
                                     ~~~~~~~~~~~~~~~~
src/user/user.controller.ts:3:64 - error TS2307: Cannot find module 'lib-server' or its corresponding type declarations.

3 import { GetUserCall, GetUserDTO, SignUpCall, SignUpDTO } from 'lib-server';
                                                                 ~~~~~~~~~~~~
src/user/user.controller.ts:5:32 - error TS2307: Cannot find module '@nestjs/microservices' or its corresponding type declarations.

5 import { MessagePattern } from '@nestjs/microservices';
                                 ~~~~~~~~~~~~~~~~~~~~~~~
src/user/user.controller.ts:12:55 - error TS2339: Property 'name' does not exist on type 'typeof UserController'.

12   private readonly logger = new Logger(UserController.name);
                                                         ~~~~
src/user/user.controller.ts:20:47 - error TS2705: An async function or method in ES5 requires the 'Promise' constructor.  Make sure you have a declaration for the 'Promise' constructor or include 'ES2015' in your '--lib' option.

20   async getUser({ id, address }: GetUserDTO): Promise<User> {
                                                 ~~~~~~~~~~~~~
src/user/user.controller.ts:26:37 - error TS2705: An async function or method in ES5 requires the 'Promise' constructor.  Make sure you have a declaration for the 'Promise' constructor or include 'ES2015' in your '--lib' option.

26   async signup(request: SignUpDTO): Promise<User> {
                                       ~~~~~~~~~~~~~
src/user/user.module.ts:1:24 - error TS2307: Cannot find module '@nestjs/common' or its corresponding type declarations.

1 import { Module } from '@nestjs/common';
                         ~~~~~~~~~~~~~~~~
src/user/user.repository.ts:7:8 - error TS2307: Cannot find module '@nestjs/common' or its corresponding type declarations.

7 } from '@nestjs/common';
         ~~~~~~~~~~~~~~~~
src/user/user.repository.ts:8:24 - error TS2307: Cannot find module '@prisma/client' or its corresponding type declarations.

8 import { Prisma } from '@prisma/client';
                         ~~~~~~~~~~~~~~~~
src/user/user.repository.ts:16:55 - error TS2339: Property 'name' does not exist on type 'typeof UserRepository'.

16   private readonly logger = new Logger(UserRepository.name);
                                                         ~~~~
src/user/user.repository.ts:20:51 - error TS2705: An async function or method in ES5 requires the 'Promise' constructor.  Make sure you have a declaration for the 'Promise' constructor or include 'ES2015' in your '--lib' option.

20   async find(where: Prisma.UserWhereUniqueInput): Promise<User> {
                                                     ~~~~~~~~~~~~~
src/user/user.repository.ts:21:24 - error TS2339: Property 'user' does not exist on type 'PrismaService'.

21     return this.prisma.user
                          ~~~~
src/user/user.repository.ts:29:47 - error TS2705: An async function or method in ES5 requires the 'Promise' constructor.  Make sure you have a declaration for the 'Promise' constructor or include 'ES2015' in your '--lib' option.

29   async create(data: Prisma.UserCreateInput): Promise<User> {
                                                 ~~~~~~~~~~~~~
src/user/user.repository.ts:30:24 - error TS2339: Property 'user' does not exist on type 'PrismaService'.

30     return this.prisma.user
                          ~~~~
src/user/user.service.ts:1:36 - error TS2307: Cannot find module '@nestjs/common' or its corresponding type declarations.

1 import { Injectable, Logger } from '@nestjs/common';
                                     ~~~~~~~~~~~~~~~~
src/user/user.service.ts:3:27 - error TS2307: Cannot find module 'lib-server' or its corresponding type declarations.

3 import { SignUpDTO } from 'lib-server';
                            ~~~~~~~~~~~~
src/user/user.service.ts:10:52 - error TS2339: Property 'name' does not exist on type 'typeof UserService'.

10   private readonly logger = new Logger(UserService.name);
                                                      ~~~~
src/user/user.service.ts:20:18 - error TS2705: An async function or method in ES5 requires the 'Promise' constructor.  Make sure you have a declaration for the 'Promise' constructor or include 'ES2015' in your '--lib' option.

20   }: SignUpDTO): Promise<User> {
                    ~~~~~~~~~~~~~

Found 38 error(s).

error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.

=======================================================================================================
Throughout the setup process I felt I was getting closer and closer to making the app run to possibly taking a shot at the scripting portion of this task but, the entire process is something I am not familiar with, my experience is more on front-end, blackbox, graybox testing, having assets I can interact with in some capacity. If this test was more locating bugs, writing them down, keeping them organized, planning out how to test, with documentation, basically anything that would be a mix of functional QA with producer duties this would've been a lock, those are my strengths. I always strive on learning and with everything I had to figure out to go from basic one line errors to receive more descriptive errors, along with setting up VSCode and Docker with installing extensions and packages, I feel good at the personal progress I made over the weekend even though I couldn't get the app to run and perform what the task asked for. I'll take my wins where I can get them, I am now setup to learn on my personal machine. Whether through books or Youtube tutorials, I can follow along a bit more informed now. 

Thank you for giving me a chance, I will make an effort to learn what it takes to get the app to run, but for today it kicked my ass. I understand there are milestones Xborg is trying to hit in the near future and I don't want to hold any of them up, knowing I don't have the skills needed to complete this task in a timely manner. 

I appreciate the opportunity and wish all of you nothing but the best. Maybe our paths will cross down the road and I'll be better skilled to take full advantage at the potential opportunity. 

Thank you once again, 

Moises Jose Zet
