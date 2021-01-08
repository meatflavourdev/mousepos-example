<script>
  import * as Y from 'yjs';
  import { WebsocketProvider } from 'y-websocket';
  import { array, map } from 'svelt-yjs';


  //import Explanation from './Explanation.svelte';
  import UndoPanel from './UndoPanel.svelte';
  import AnimalMap from './AnimalMap.svelte';
  import UserMap from './UserMap.svelte';

  // All Yjs types must be embedded in a Y.Doc
  const ydoc = new Y.Doc();

  const wsUrl = 'wss://2dfc6998bfab.ngrok.io';
  // Connect our Y.Doc to the sync server. Note that you could also use p2p
  // via webrtc (due to Yjs' CRDT convergence algorithm, no server necessary).
  new WebsocketProvider(wsUrl, 'example', ydoc);

  // Create a Y.Array<string> in the Y.Doc
  const yarray = ydoc.getArray('list');

  // Create a Y.Map<number> in the Y.Doc
  const ymap = ydoc.getMap('dict');

  // Create a Y.Map<number> in the Y.Doc
  const userMap = ydoc.getMap('userdict');

  // Generate two Svelte readable stores from the Y types we just added to the Y.Doc
  const list = array.readable(yarray);
  const dict = map.readable(ymap);
  const userdict = map.readable(userMap);

  // Add undo/redo manager
  const undoManager = new Y.UndoManager([list.y, dict.y], {
    captureTimeout: 0,
  });
</script>

<style>
  page {
    display: block;
    margin: 0;
    height: 100%;
  }
  action,
  subaction {
    display: block;
    margin: 0 32px;
  }
  action {
    text-align: center;
    font-size: 150%;
    color: var(--punch);
    margin: 48px auto 0 auto;
  }
  subaction {
    margin-bottom: 48px;
  }
  subaction ul {
    margin: 8px 0;
  }
</style>

<page>

  <content>

    <!-- <UndoPanel {undoManager} /> -->

    <!-- <AnimalMap map={dict} /> -->

    <UserMap map={userdict} />
  </content>
</page>
