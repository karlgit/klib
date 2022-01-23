### react-dom 加载流程

const rootELement = document.getElementById("root");
1. ReactDOM.createRoot(rootElement)
    1. createContainer():FiberRoot
       1. createFiberRoot():FiberRoot
          1. root = new FiberRootNode():FiberRoot
          2. createHostRootFiber():Fiber
             1. createFiber():Fiber
                1. return new FiberNode():Fiber
          3. root.current = uninitializedFiber
          4. uninitializedFiber.stateNOde = root
          5. initializeUpdateQueue
          6. return root;
    2. markContainerAsRoot
    3. listenToAllSupportedEvents 
    4. return new ReactDOMRoot(root):ReactDOMRoot

2. root.render(<App callback={()=>{}} />)
   1. __DEV__ 
   2. updateContainer()
      1. requestUpdateLane
      2. markRenderScheduled
      3. getContextForSubtree
      4. createUpdate
      5. callback
      6. enqueueUpdate
      7. scheduleUpdateOnFiber
         1. ensureRootIsScheduled
            1. scheduleSyncCallback if SyncLane
            2. scheduleMicrotask if supportsMicrotasks
            3. scheduleCallback
      8. entangleTransitions
      9. return lane