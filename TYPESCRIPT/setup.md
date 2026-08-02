## Step 1: Create a folder
TS Practicals/

## Step 2: Initialize npm
```sh
npm init -y
```
This creates : package.json

## Step 3: Install TypeScript
```sh
npm install -D typescript
```
This installs TypeScript as a dev dependency.

## Step 4: Create a TypeScript configuration
```sh
npx tsc --init
```
This creates : tsconfig.json

## Step 5: Create your TypeScript file
index.ts
```sh
let name: string = "Ajith";

console.log(name);
```

## Step 6: Compile TypeScript
Run:
```sh
npx tsc
```
TypeScript converts : index.ts -> index.js

## Step 7: Run the JavaScript file
```sh
node index.js
```
Output : Ajith

