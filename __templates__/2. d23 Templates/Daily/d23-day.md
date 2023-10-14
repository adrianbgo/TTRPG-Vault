<%*
const title = await tp.system.prompt("Enter Room Title");
let event = moment();
const execution_value = await tp.system.suggester(["Yes", "No"], ["true", "false"], false, "Writing for today?");
if ( execution_value == "false" ) {
    event = moment(await tp.system.prompt("Enter Date in format: YYYY-MM-DD"));
}
let the_day  = event.format("YYYY-MM-DD");
let the_week = event.format("W");
let the_year = event.format("YY");
console.log("Event [%o]: %o, %o, %o, %o", event.toString('YYYY-MM-DD'), the_day, the_week, the_year);

await tp.file.rename(the_day);

let status =  await tp.system.suggester(
  ["done", "needs-revision", "unfinished", "started", "draft"], 
  ["100", "80", "60", "40", "20"], 
  true);

const source = await tp.system.suggester(["5e", "a5e", "pf2e", "wwn"], ["5e", "a5e", "pf2e", "wwn"], false, "Choose System");
-%>
<%"---"%>
type: dungeon<%the_year%>-day
tags:
  - dungeon<%the_year%>/day
  - <%source%>
date: <%the_day%>
room: <%the_room%>
week: <%the_week%>
aliases: [<%title%>, <%the_room%>]
status: <%status%>
title: <%title%>
cssclasses: cards
<%"---"%>

