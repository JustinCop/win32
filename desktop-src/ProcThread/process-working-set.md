---
Description: The working set of a program is a collection of those pages in its virtual address space that have been recently referenced.
ms.assetid: 6017ef59-d2e9-4245-a406-8965024dbb35
title: Process Working Set
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# Process Working Set

The *working set* of a program is a collection of those pages in its virtual address space that have been recently referenced. It includes both shared and private data. The shared data includes pages that contain all instructions your application executes, including those in your DLLs and the system DLLs. As the working set size increases, memory demand increases.

A process has an associated minimum working set size and maximum working set size. Each time you call [**CreateProcess**](/windows/desktop/api/WinBase/nf-processthreadsapi-createprocessa), it reserves the minimum working set size for the process. The virtual memory manager attempts to keep enough memory for the minimum working set resident when the process is active, but keeps no more than the maximum size.

To get the requested minimum and maximum sizes of the working set for your application, call the [**GetProcessWorkingSetSize**](/windows/desktop/api/WinBase/nf-winbase-getprocessworkingsetsize) function.

The system sets the default working set sizes. You can also modify the working set sizes using the [**SetProcessWorkingSetSize**](/windows/desktop/api/WinBase/nf-winbase-setprocessworkingsetsize) function. Setting these values is not a guarantee that the memory will be reserved or resident. Be careful about requesting too large a minimum or maximum working set size, because doing so can degrade system performance.

To obtain the current or peak size of the working set for your process, use the [**GetProcessMemoryInfo**](https://www.bing.com/search?q=**GetProcessMemoryInfo**) function.

## Related topics

<dl> <dt>

[Memory Performance Information](https://msdn.microsoft.com/windows/desktop/b27ca747-8fd2-4267-9979-4e2e14a5a19f)
</dt> <dt>

[Working Set](https://msdn.microsoft.com/windows/desktop/ff05276a-1d40-4844-b649-10e32e3f1937)
</dt> </dl>

 

 


