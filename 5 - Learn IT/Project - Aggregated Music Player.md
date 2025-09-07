## 1. Mopidy + Extensions

An extensible Python music server with a rich web-UI ecosystem.

- **Backends**
    
    - `Mopidy-Spotify` (requires Premium)
        
    - `Mopidy-Tidal` (community plugin)
        
    - `Mopidy-YouTube`
        
    - Local filesystem/library
        
- **Recommended Web UIs**
    
    - [Iris](https://github.com/jaedb/Iris) – full-featured, mobile-friendly
        
    - [MusicBox Webclient](https://github.com/pimusicbox/mopidy-musicbox-webclient) – lightweight
        
- **Pros**
    
    - One server, multiple sources
        
    - Actively maintained, Docker images available
        
- **Cons**
    
    - Some plugins are community-driven (spotty support)
        
    - Spotify & Tidal require credentials/premium
        

---

## 2. Jellyfin with Music Plugins

An all-in-one media server (videos, music, live TV) that also supports music-service plugins:

- **Core**: libraries of your local tracks
    
- **Plugins**:
    
    - Spotify playlists (read-only)
        
    - Tidal (via third-party plugin)
        
    - YouTube (as “music videos”)
        
- **Web GUI**: full Jellyfin dashboard, customisable skins
    
- **Pros**
    
    - Single app handles all your media
        
    - Active community, well-maintained
        
- **Cons**
    
    - Streaming integrations can feel kludgy
        
    - Tidal/YouTube plugins are unofficial
        

---

## 3. Navidrome + Mopidy Hybrid

- **Navidrome** for your local and Subsonic-API-compatible clients (very lightweight)
    
- **Mopidy** alongside for Spotify/Youtube/Tidal
    
- Point your favorite web UI (Iris, Subbonsic, DSub) at Navidrome for local, and Iris at Mopidy for streaming sources
    
- **Pros**: best-of-both worlds, rock-solid local library
    
- **Cons**: two services to maintain
    

---

## 4. Funkwhale

A federated audio-sharing platform that can host your uploads and pull in “remote” instances.

- **Local library** + “federation” across other Funkwhale servers
    
- Has a Docker-based web UI
    
- **Pros**
    
    - Great UI for browsing collections
        
    - Social/federation features
        
- **Cons**
    
    - No native Spotify/Tidal backends (you’d have to rip or sync manually)