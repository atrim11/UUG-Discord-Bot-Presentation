# UUG-Discord-Bot-Presentation

##  #1 Create Discord Bot 
  1. go to Discord Developer Portal https://discord.com/developers/applications 
  2. Then Click New Application Button
  3. Give Name and Create 
  4. Click bots Tab on sidebard 
  5. Add Bot
  6. Then give all check marks under Privileged Gateway Intents 
## #2 Create Autocode Account
  1. Create an account on Autocode https://autocode.com/signup?invite_code=AvwUJZNE6FQeQftb
  2. Create New Web Service
  3. Create New project 
  4. Click the HTTP request or webhook  
  5. Discord - message.create.prefix - !ask 

## #3 Link Discord To Autocode
  1. Linked Resources in bottom left click link button
  2. Choose Discord as the API Scource 
  3. Get Client ID and Client Sectret From The developer Portal 
  4. Copy the Redirect URL and paste it and add it on your Discord auth page as seen in the modal.
  5. Input your bot token on the next screen and click the blue Finish button.
  6. Follow Discord's authentication instructions. You'll be asked to choose a server to add your bot to.
  
## #4 Link Google Sheet to Autocode
  1. Linked Resources in bottom left click link button
  2. Choose Google Sheet as the API Scource 
  3. Create a new google sheet
  4. Name top two as "Question" and "Answer"
  5. add this block of code
  ```
  const lib = require("lib")({ token: process.env.STDLIB_SECRET_TOKEN });

let question = context.params.event.content.split(" ").slice(1).join(" ");

if (!question) {
  await lib.discord.channels["@0.3.0"].messages.create({
    channel_id: `${context.params.event.channel_id}`,
    content: [
      `Whoops! Looks like you didn't use the prefix command properly`,
      `You must use the prefix command followed by a question`,
      "",
      "To view a list of questions I can answer use the command **!help**",
      "**For example: !ask How to change bot status?**",
    ].join("\n"),
  });
  return;
}

let frequencyQuery = await lib.googlesheets.query["@0.3.0"].distinct({
  range: `A:C`,
  bounds: `FIRST_EMPTY_ROW`,
  where: [
    {
      Question__contains: question,
    },
  ],
  field: `Frequency`,
});
  ```
  
## #5 Create Your Slash Command 
  1. Now you need to set up the slash command https://autocode.com/tools/discord/command-builder/
  2. Link your Discord bot account to the command builder. If you've previously linked one, you can click the green choose button, or link a new resource.
