--[[
    Roblox server ip port and datacenter grabber made by sufi#1337
    
    (The roblox server is waiting packets go send!!!)
]]

getgenv().RobloxCookie = "" -- Add your roblox cookie here || copy it exactly as it is

local request = syn.request or request
local gameid = game.PlaceId
local jobid = game.JobId
local http = game:GetService("HttpService")
local ip
local port
local dataCenterID
local notifications = loadstring(game:HttpGet("https://pastebin.com/raw/kSLQbpjV"))()

local reqdata = {
    ['placeId'] = gameid,
    ['gameId'] = jobid,
    ['isPlayTogetherGame'] = false
}

reqdata = http:JSONEncode(reqdata)

local headers = {
    ['Content-Type'] = "application/json",
    ['Cookie'] = string.format(".ROBLOSECURITY=%s", RobloxCookie),
    ['User-Agent'] = 'Roblox/WinInet'
}

local Payload = {Url = 'https://gamejoin.roblox.com/v1/join-game-instance', Body = reqdata, Method = "POST", Headers = headers}
local response = request(Payload)
if response.StatusCode == 200 then
    response = response.Body
    response = http:JSONDecode(response)
    if response.message then
        if string.find(response.message, 'Unable to join') then
            notifications.prompt('Lego Server Data\nBy sufi#1337', 'There was an error. Please check your cookie.')
            return
        end
    end
    for i,v in pairs(response) do
        if i == 'joinScript' then
            for i1,v1 in pairs(v) do
                if i1 == 'MachineAddress' then
                    ip = v1
                elseif i1 == 'ServerPort' then
                    port = v1
                elseif i1 == 'DataCenterId' then
                    dataCenterID = v1
                end
            end
        end
    end
else
    notifications.prompt('Lego Server Data\nBy sufi#1337', 'There was an error. Please check your cookie. Status Code: '..response.StatusCode)
    return
end

local msg = 'Server IP: '..ip..'\nServer Port: '..port..'\nData Center ID: '..dataCenterID

notifications.prompt('Lego Server Data By sufi#1337', msg..'\nData copied to clipboard!')
setclipboard(msg)
