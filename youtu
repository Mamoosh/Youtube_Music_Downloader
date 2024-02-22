import string
import random
from pytube import YouTube
from tkinter import Tk, Label, Entry, Button, StringVar, messagebox, OptionMenu, filedialog

def download(url, quality, download_path):
    try:
        youtube_content = YouTube(url)
        audio_streams = youtube_content.streams.filter(only_audio=True)
        audio_streams = sorted(audio_streams, key=lambda x: x.abr)
        qualities = [stream.abr for stream in audio_streams]
        stream = audio_streams[qualities.index(quality)]
        random_string = ''.join(random.choices(string.ascii_letters + string.digits, k=8))
        file_name = f"music_{random_string}.mp3"
        stream.download(output_path=download_path, filename=file_name)
        messagebox.showinfo("Success", "Download completed successfully!")
    except Exception as e:
        messagebox.showerror("Error", f"Download failed: {str(e)}")

def select_folder():
    folder_selected = filedialog.askdirectory()
    return folder_selected

def main():
    window = Tk()
    window.geometry("400x200")  # Makes the window bigger
    window.title("YouTube Downloader")
    window.configure(bg='light blue')
    Label(window, text="Your Url: ", bg='light blue').grid(row=0, sticky='w', padx=5, pady=5)
    url = StringVar()
    url_entry = Entry(window, textvariable=url)
    url_entry.grid(row=0, column=1, sticky='we', padx=5, pady=5)
    Label(window, text="Quality: ", bg='light blue').grid(row=1, sticky='w', padx=5, pady=5)
    quality = StringVar(window)
    quality.set("Select Quality") # default value
    quality_menu = OptionMenu(window, quality, "50kbps", "70kbps", "128kbps", "160kbps")
    quality_menu.grid(row=1, column=1, sticky='we', padx=5, pady=5)
    Label(window, text="Download Path: ", bg='light blue').grid(row=2, sticky='w', padx=5, pady=5)
    download_path = StringVar()
    download_path_entry = Entry(window, textvariable=download_path)
    download_path_entry.grid(row=2, column=1, sticky='we', padx=5, pady=5)
    Button(window, text="Select Folder", command=lambda: download_path.set(select_folder())).grid(row=2, column=2, sticky='w', padx=5, pady=5)
    Button(window, text="      Download      ", command=lambda: download(url.get(), quality.get(), download_path.get())).grid(row=3, column=0, sticky='w', padx=10, pady=30)
    window.columnconfigure(1, weight=1)  # Makes column 1 expandable
    window.mainloop()

if __name__ == '__main__':
    main()  
