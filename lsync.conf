settings {
        logfile ="/var/log/lsyncd/lsyncd.log",
        statusFile ="/var/log/lsyncd/lsyncd.status",
        inotifyMode = "CloseWrite",
        maxProcesses = 7,
        -- nodaemon =true,
       }

local startup =
[[
cp -r ^source* ^target &&
find ^target -name "*.strm" -exec sed -i "s#DOCKER_ADDRESS#http://192.168.1.6:5678#g" {} \;
]]

sync {
      source = "/home/axs/app/resilio/sync/每日更新/电影",
      target = "/home/axs/app/lsync/每日更新/电影",
      onDelete = "rm -rf ^targetPathname",
      onMove   = "mv ^o.targetPathname ^d.targetPathname",
      onStartup = startup,
      onCreate = function(event)
        if event.pathname:match("%.strm$") then
          local cmd = 'cp '..event.sourcePath..' /dev/stdout | sed "s#DOCKER_ADDRESS#http://192.168.1.6:5678#g" > '..event.targetPath
          spawnShell(event, cmd)
        elseif not event.pathname:match("%.sync") then
          local cmd = 'cp -r '..event.sourcePath..' '..event.targetPath
          spawnShell(event, cmd)
        end
      end
}
