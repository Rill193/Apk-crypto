import random
from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.button import Button
from kivy.uix.textinput import TextInput
from kivy.uix.scrollview import ScrollView
from kivy.clock import Clock

class BitcoinWalletApp(App):
    def __init__(self):
        super().__init__()
        self.wallets = set()
        self.bitcoins = set()
        self.is_searching = False
        self.address_count = 0
        self.bitcoin_count = 0

    def generate_wallet(self):
        alphabet = "123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz"
        length = 34
        return ''.join(random.choices(alphabet, k=length))

    def generate_bitcoin_amount(self):
        return round(random.uniform(0.1, 1), 2)

    def stop_search(self, instance):
        self.is_searching = False

    def generate_and_display_wallet(self, dt):
        if self.is_searching:
            wallet = self.generate_wallet()
            bitcoin_amount = self.generate_bitcoin_amount()
            self.address_count += 1
            self.wallets.add(wallet)
            if self.address_count % 100 == 0:
                self.bitcoin_count += bitcoin_amount
                self.update_bitcoin_table(self.bitcoin_count)
            self.console.text += wallet + '\n'

    def search_data(self, instance):
        if not self.is_searching:
            self.is_searching = True
            self.console.text = ""  # Clear console before starting a new search
            self.address_count = 0  # Reset address count
            Clock.schedule_interval(self.generate_and_display_wallet, 0.01)

    def update_bitcoin_table(self, amount):
        self.bitcoin_table.text = f"Найдено биткоинов: {amount} BTC"

    def scroll_to_bottom(self, instance):
        self.console_scroll_view.scroll_y = 0

    def output_address(self, instance):
        address = self.address_input.text
        if address:
            self.console.text += address + '\n'
            self.address_input.text = ""  # Clear the text input after outputting the address

    def build(self):
        root = BoxLayout(orientation='vertical')

        # Верхняя часть с тремя кнопками
        top_layout = BoxLayout(orientation='horizontal', size_hint_y=0.1)
        search_button = Button(text="Поиск", background_color=(0, 0.5, 1, 1))
        search_button.bind(on_press=self.search_data)
        stop_button = Button(text="Стоп", background_color=(1, 0.5, 0, 1))
        stop_button.bind(on_press=self.stop_search)
        top_layout.add_widget(search_button)
        top_layout.add_widget(stop_button)
        root.add_widget(top_layout)

        # Консоль и скролл
        self.console = TextInput(readonly=True, multiline=True)
        self.console.height = 400
        self.console_scroll_view = ScrollView()
        self.console_scroll_view.add_widget(self.console)
        root.add_widget(self.console_scroll_view)

        # Нижняя часть с кнопкой вывода адреса
        bottom_layout = BoxLayout(orientation='horizontal', size_hint_y=0.1)
        self.address_input = TextInput(hint_text='Введите адрес', multiline=False)
        output_button = Button(text="Вывод", background_color=(0, 0.5, 1, 1))
        output_button.bind(on_press=self.output_address)
        bottom_layout.add_widget(self.address_input)
        bottom_layout.add_widget(output_button)
        root.add_widget(bottom_layout)

        # Таблица для биткоинов
        self.bitcoin_table = TextInput(readonly=True, multiline=False)
        root.add_widget(self.bitcoin_table)

        return root

if __name__ == "__main__":
    BitcoinWalletApp().run()
