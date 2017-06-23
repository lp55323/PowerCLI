 function LoadSnapins(){ 
   $snapinList = @( "VMware.VimAutomation.Core", "VMware.VimAutomation.Vds", "VMware.VimAutomation.License", "VMware.DeployAutomation", "VMware.ImageBuilder", "VMware.VimAutomation.Cloud", "VMware.VimAutomation.Storage")  

   $loaded = Get-PSSnapin -Name $snapinList -ErrorAction SilentlyContinue | % {$_.Name} 
   $registered = Get-PSSnapin -Name $snapinList -Registered -ErrorAction SilentlyContinue  | % {$_.Name} 
   $notLoaded = $registered | ? {$loaded -notcontains $_} 
   
   foreach ($snapin in $registered) { 
      if ($loaded -notcontains $snapin) { 
         Add-PSSnapin $snapin 
      } 
} 
} 
LoadSnapins 
