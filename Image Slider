import tkinter as tk

class Cards:
    def __init__(self,root):
        self.root=root
        self.root.title('Expanding Cards')
        self.root.geometry('800x400')
        self.root.configure(bg='#1e1e24')

        self.collapsed_width=80
        self.expanded_width=400
        self.card_height=300
        self.animation_speed=15
        self.active_card=None

        self.main_frame=tk.Frame(self.root,bg='#1e1e24')
        self.main_frame.pack(expand=True)

        btn_frame=tk.Frame(root,bg='#1e1e24')
        btn_frame.pack(pady=20)

        prev_btn=tk.Button(btn_frame,text='< Prev',font=('Arial',12,'bold'),bg='#ffca3a',fg='#1e1e24',command=self.prev_card)
        prev_btn.pack(side='left',padx=10)

        next_btn=tk.Button(btn_frame,text='Next >',font=('Arial',12,'bold'),bg='#ffca3a',fg='#1e1e24',command=self.next_card)
        next_btn.pack(side='left',padx=10)
        
        card_data=[('Card 01','#ff595e','welcome to our Card one!\nSmooth sliding animations'),
                   ('Card 02','#ffca3a','this is card two.\nbuilt with pure python code.'),
                   ('Card 03','#8ac926','here is card three. \nNo dowloaded photos needed!')]
        self.cards=[]
        for title,color,text in card_data:
            card_frame=tk.Frame(self.main_frame,bg=color,width=self.collapsed_width,height=self.card_height)
            card_frame.pack(side='left',padx=10)
            card_frame.pack_propagate(False)
            title_lbl=tk.Label(card_frame,text=title,font=('Arial',14,'bold'),bg=color,fg='white')
            title_lbl.pack(pady=20)

            content_lbl=tk.Label(card_frame,text=text,font=('Arial',11),bg=color,fg=color,justify='center')
            content_lbl.pack(expand=True,fill='both',padx=10,pady=10)
            card_info={'frame':card_frame,'title':title_lbl,'content':content_lbl,'color':color}
            self.cards.append(card_info)

            card_frame.bind('<Button-1>',lambda e,c=card_info: self.on_card_click(c))
            title_lbl.bind('<Button-1>',lambda e,c=card_info: self.on_card_click(c))
            content_lbl.bind('<Button-1>',lambda e,c=card_info: self.on_card_click(c))


        self.on_card_click(self.cards[0])

    def on_card_click(self,clicked_card):
        if self.active_card==clicked_card:
            return
        if self.active_card:
            self.active_card['content'].config(fg=self.active_card['color'])
            self.animate_card(self.active_card,self.collapsed_width)

        self.active_card=clicked_card
        self.animate_card(self.active_card,self.expanded_width)
        self.active_card['content'].config(fg="white")

    def animate_card(self,card,target_width):
        current_width=card['frame'].winfo_width()
        if current_width<=1:
            current_width=int(card['frame'].cget('width'))

        if current_width<target_width:
            new_width=min(current_width+self.animation_speed,target_width)
            card['frame'].config(width=new_width)
            self.root.after(10,lambda: self.animate_card(card,target_width))

        elif current_width>target_width:
            new_width=max(current_width-self.animation_speed,target_width)
            card['frame'].config(width=new_width)
            self.root.after(10,lambda: self.animate_card(card,target_width))

    def prev_card(self):
        current_idx=self.cards.index(self.active_card)
        pre_idx=(current_idx-1%len(self.cards))
        self.on_card_click(self.cards[pre_idx])

    def next_card(self):
        current_idx=self.cards.index(self.active_card)
        next_idx=(current_idx+1)%len(self.cards)
        self.on_card_click(self.cards[next_idx])



if __name__=='__main__':
    window=tk.Tk()
    app=Cards(window)
    window.mainloop()

