# UI Changes Hints

UI code changes may be limited to ui/src/views/NetworkCustomizations/LoRa/, Network.js and Application.js.  Maybe more if we really want to support every level of data with custom networkProtocol fields, but I would recommend against that unless they really want us to do it and we have time left over.

These get called by ui/src/views/NetworkCustomizations/NetworkSpecificUI.js, which is called by the ui/src/views/\*/Create\*.js files (for creates, right?), or the ui/src/components/\*Form.js files, included into the ui/src/views/\*/\*Layout.js files (for updates).  It's goofy to do it both ways, but we just followed the model that was already set up by Orne for the LoraAppServer, which he has since changed, but we didn't bother.

The Stores are where the rest calls are done.  Pretty basic and common stuff, I think.

The only tricky thing MAY be passing query parameters down the chain, and where the custom field handling happens.

Give a shout if something isn't clear.

