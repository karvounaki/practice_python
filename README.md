# practice_python
import codecademylib
import pandas as pd

visits = pd.read_csv('visits.csv',
                     parse_dates=[1])
cart = pd.read_csv('cart.csv',
                   parse_dates=[1])
checkout = pd.read_csv('checkout.csv',
                       parse_dates=[1])
purchase = pd.read_csv('purchase.csv',
                       parse_dates=[1])

print(visits.head())
print(cart.head())
print(checkout.head())
print(purchase.head())

visits_cart=pd.merge(visits, cart, how='left')
print (visits_cart.info())
print(len(visits_cart))
print(len(visits_cart[visits_cart.cart_time.isnull()]))
users_not_cart=(len(visits_cart[visits_cart.cart_time.isnull()])/float(len(visits_cart)))*100
print users_not_cart

cart_checkout=pd.merge(cart, checkout, how='left')
print(len(visits_cart))
print(len(cart_checkout[cart_checkout.checkout_time.isnull()]))
users_not_checkout=(len(cart_checkout[cart_checkout.checkout_time.isnull()])/float(len(cart_checkout)))*100
print(users_not_checkout)

all_data=visits.merge(cart, how='left').merge(checkout, how='left').merge(purchase, how='left')

print(all_data.head())
print(len(all_data))
print(len(all_data[all_data.purchase_time.isnull()]))
users_not_purchase=(len(all_data[all_data.purchase_time.isnull()])/float(len(all_data)))*100
print(users_not_purchase)

all_data['time_to_purchase']=all_data.purchase_time-all_data.visit_time

print(all_data.time_to_purchase)

print(all_data.time_to_purchase.mean())
