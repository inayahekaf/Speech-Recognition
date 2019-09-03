# Speech-Recognition
from tkinter import *
from tkinter import ttk
import webbrowser
import speech_recognition as sr
from pygame import mixer
root = Tk()
root.title('Speech Recognition')
root.configure(background='#808080')
root.geometry('500x350+200+250')
root.iconbitmap('D:\\KP\\mic.png') 
photo =PhotoImage(file='mic3.png').subsample(15,15)
label1 = ttk.Label(root, text=' ', font='none 10', background='#808080')
label1.pack()
photo1 =PhotoImage(file='its.png').subsample(15,15)
label = ttk.Label(root, image=photo1, background='#808080')
label.pack()
label2 = ttk.Label(root, text='SPEECH RECOGNITION', foreground='#FFC0CB', font='none 20 bold', background='#808080')
label2.pack()
label3 = ttk.Label(root, text='by : ', foreground='#FFC0CB', font='none 8 italic', background='#808080')
label3.pack()
label4 = ttk.Label(root, text='Inayah Eka Firdausi (06111540000018)', foreground='#FFC0CB', font='none 10 italic', background='#808080')
label4.pack()
label5 = ttk.Label(root, text='Izah Amalia (06111540000068)', foreground='#FFC0CB', font='none 10 italic', background='#808080')
label5.pack()
label6 = ttk.Label(root, text=' ', font='none 8 italic', background='#808080')
label6.pack()
label7 = ttk.Label(root, text='Choose the language then click the microphone', foreground='#FFC0CB', background='#808080')
label7.pack()
entry1 = ttk.Entry(root, width=80)
entry1.pack()
btn2 = StringVar()    
def buttonClick(): 
    mixer.init()
    mixer.music.load('siri2.mp3')
    mixer.music.play() 
    r = sr.Recognizer()
    r.pause_thereshold = 0.7
    r.energy_thereshold = 400 
    with sr.Microphone() as source :
        try :
            audio = r.listen(source, timeout=5)
            if btn2.get() == 'eng' :
                 message = str(r.recognize_google(audio))
            elif btn2.get() == 'id' :
                 message = str(r.recognize_google(audio, language='id-ID'))
            elif btn2.get() == 'kor' :
                 message = str(r.recognize_google(audio, language='ko-KR'))
            elif btn2.get() == 'jp' :
                 message = str(r.recognize_google(audio, language='ja-JP'))
            else :
                pass
            mixer.music.load('siri.mp3')
            mixer.music.play()
            entry1.focus()
            entry1.delete(0, END)
            entry1.insert(0, message)
        except sr.UnknownValueError :
            print('Google Speech Recognition could not understand audio') 
        except sr.RequestError as e :
            print('Could not request result from Google Speech Recognition Server') 
        else :
            pass
button1 = Button(root, image=photo, command=buttonClick, bd=0, background='#808080', activebackground='#FFC0CB', overrelief='groove', relief='sunken')
button1.pack()
button2 = ttk.Radiobutton(root, text="English", value='eng', variable=btn2)
button2.pack(side=LEFT, expand=1)
button3 = ttk.Radiobutton(root, text="Indonesia", value='id', variable=btn2)
button3.pack(side=LEFT, expand=1)
button4 = ttk.Radiobutton(root, text="Korea", value='kor', variable=btn2)
button4.pack(side=LEFT, expand=1)
button5 = ttk.Radiobutton(root, text="Japan", value='jp', variable=btn2)
button5.pack(side=LEFT, expand=1)
entry1.focus()
root.mainloop()
