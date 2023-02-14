<template>
  <div class="w-full min-h-screen font-sans text-gray-900 bg-gray-50 flex">
    <aside class="py-6 px-10 w-64 border-r border-gray-200">
      <img src="" alt="" class="w-28" />
      <ul v-for="group in sidebar" class="flex flex-col gap-y-6 pt-20">
        <li v-for="item in group">
          <a
            href="#"
            class="flex gap-x-4 items-center py-2 text-gray-500 hover:text-indigo-600 group"
          >
            <span
              class="absolute w-1.5 h-8 bg-indigo-600 rounded-r-full left-0 scale-y-0 -translate-x-full group-hover:scale-y-100 group-hover:translate-x-0 transition-transform ease-in-out"
            />
            <Component :is="item.icon" class="w-6 h-6 fill-current" />
            <span>{{ item.name }}</span>
          </a>
        </li>
      </ul>
    </aside>

    <main class="flex-1 pb-8">
      <div class="flex items-center justify-between py-7 px-10">
        <div>
          <h1 class="text-2xl font-semibold leading-relaxed text-gray-800">LƯƠNG NGỌC HUY MALL</h1>
          <p class="text-sm font-medium text-gray-500">
          </p>
        </div>
        <button
          class="inline-flex gap-x-2 items-center py-2.5 px-6 text-white bg-indigo-600 rounded-xl hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-1"
        >
          <PlusIcon class="w-6 h-6 fill-current" />
          <span class="text-sm font-semibold tracking-wide">Create Item</span>
        </button>
      </div>

      <ul class="flex gap-x-24 items-center px-4 border-y border-gray-200">
        <li v-for="item in status">
          <button
            class="flex gap-x-2 items-center py-5 px-6 text-gray-500 hover:text-indigo-600 relative group"
          >
            <Component :is="item.icon" class="w-6 h-6 fill-current" />
            <span class="font-medium"> {{ item.name }} </span>
            <span
              class="absolute w-full h-0.5 left-3 bg-indigo-600 rounded bottom-0 scale-x-0 group-hover:scale-x-100 transition-transform ease-in-out"
            />
          </button>
        </li>
      </ul>

      <table class="w-full border-b border-gray-200">
        <thead>
          <tr class="text-sm font-medium text-gray-700 border-b border-gray-200">
            <td class="pl-10">
              <div class="flex items-center gap-x-4">
                <input
                  type="checkbox"
                  class="w-6 h-6 text-indigo-600 rounded-md border-gray-300"
                  indeterminate="indeterminate"
                />
                <span>Product Name</span>
              </div>
            </td>
            <td class="py-4 px-4 text-center">Pricing</td>
            <td class="py-4 px-4 text-center">Sold</td>
            <td class="py-4 px-4 text-center">Rating</td>
            <td class="py-4 px-4 text-center">Origin</td>
            <td class="py-4 pr-10 pl-4 text-center">
              <FilterIcon class="w-6 h-6 fill-current" />
            </td>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="product in products"
            class="hover:bg-gray-100 transition-colors group"
          >
            <td class="flex gap-x-4 items-center py-4 pl-10">
              <input
                type="checkbox"
                class="w-6 h-6 text-indigo-600 rounded-md border-gray-300"
              />
              <img
                :src="product.imageUrl"
                alt=""
                class="w-40 aspect-[3/2] rounded-lg object-cover object-top border border-gray-200"
              />
              <div>
                <a href="#" class="text-lg font-semibold text-gray-700">
                  {{ product.name }}
                </a>
                <div class="font-medium text-gray-400">{{ product.category }}</div>
              </div>
            </td>
            <td class="font-medium text-center">${{ product.price }}</td>
            <td class="font-medium text-center">{{ product.sold }}</td>
            <td class="text-center">
              <span class="font-medium">{{ product.rating }}</span>
              <span class="text-gray-400">/5</span>
            </td>
            <td>
              <div class="flex gap-x-2 justify-center items-center">
                <a
                  href="#"
                  v-for="icon in product.platformIcons"
                  class="p-2 bg-gray-200 rounded-md hover:bg-gray-300"
                >
                  <Component :is="icon" class="w-6 h-6" />
                </a>
              </div>
            </td>
            <td>
              <span class="inline-block w-20 group-hover:hidden">
                {{ product.createdAt }}
              </span>
              <div
                class="hidden group-hover:flex group-hover:w-20 group-hover:items-center group-hover:text-gray-500 group-hover:gap-x-2"
              >
                <button class="p-2 hover:rounded-md hover:bg-gray-200">
                  <PencilIcon class="w-6 h-6 fill-current" />
                </button>
                <button class="p-2 hover:rounded-md hover:bg-gray-200">
                  <TrashIcon class="w-6 h-6 fill-current" />
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>

      <div class="flex gap-x-2 justify-center pt-8">
        <button class="flex justify-center items-center w-8 h-8">
          <ChevronLeftIcon
            class="w-6 h-6 to-gray-800 stroke-current hover:text-indigo-600"
          />
        </button>
        <button
          v-for="i in 6"
          class="flex items-center justify-center w-8 h-8 font-medium rounded-full"
          :class="
            i === 1 ? 'bg-gray-800 text-white' : 'text-gray-400 hover:text-indigo-600'
          "
        >
          {{ i }}
        </button>
        <button class="flex justify-center items-center w-8 h-8">
          <ChevronRightIcon
            class="w-6 h-6 to-gray-800 stroke-current hover:text-indigo-600"
          />
        </button>
      </div>
    </main>
  </div>
</template>
<script setup>
import OverviewIcon from "./icons/overview.svg";
import ShoppingBagIcon from "./icons/shopping-bag.svg";
import GraphIcon from "./icons/graph.svg";
import CalendarIcon from "./icons/calendar.svg";
import WalletIcon from "./icons/wallet.svg";
import FileIcon from "./icons/file.svg";
import ChatIcon from "./icons/chat.svg";
import GroupChatIcon from "./icons/group-chat.svg";
import SettingsIcon from "./icons/settings.svg";
import LogoutIcon from "./icons/logout.svg";
import PlusIcon from "./icons/plus.svg";
import LayersIcon from "./icons/layers.svg";
import DraftIcon from "./icons/draft.svg";
import InvisibleIcon from "./icons/invisible.svg";
import RejectedIcon from "./icons/rejected.svg";
import MailIcon from "./icons/mail.svg";
import FilterIcon from "./icons/filter.svg";
import SketchIcon from "./icons/sketch.svg";
import PencilIcon from "./icons/pencil.svg";
import TrashIcon from "./icons/trash.svg";
import ChevronLeftIcon from "./icons/chevron-left.svg";
import ChevronRightIcon from "./icons/chevron-right.svg";
import AppleIcon from "./icons/apple.svg"
import SamsungIcon from "./icons/samsung.svg"
import HuaweiIcon from "./icons/huawei.svg"
import XiaomiIcon from "./icons/xiaomi.svg"

const sidebar = [
  [
    { name: "Overview", icon: OverviewIcon },
    { name: "Products", icon: ShoppingBagIcon },
    { name: "Analytics", icon: GraphIcon },
    { name: "Schedule", icon: CalendarIcon },
    { name: "Payout", icon: WalletIcon },
    { name: "Statements", icon: FileIcon },
  ],
  [
    { name: "Help", icon: ChatIcon },
    { name: "Community", icon: GroupChatIcon },
    { name: "Settings", icon: SettingsIcon },
    { name: "Logout", icon: LogoutIcon },
  ],
];

const status = [
  { name: "Published", icon: LayersIcon },
  { name: "Draft", icon: DraftIcon },
  { name: "Hidden", icon: InvisibleIcon },
  { name: "Rejected", icon: RejectedIcon },
  { name: "Under Review", icon: MailIcon },
];

const products = [
  {
    name: "Iphone 14 promax",
    category: "IOS",
    imageUrl: "/img/ip14.png",
    price: 1000,
    sold: 793,
    rating: 4.9,
    platformIcons: [AppleIcon],
    createdAt: "12/01/22",
  },
  {
    name: "Xiaomi Note 9",
    category: "ANDROID",
    imageUrl: "/img/xiaomi.png",
    price: 200,
    sold: 34,
    rating: 4.4,
    platformIcons: [XiaomiIcon],
    createdAt: "10/01/22",
  },
  {
    name: "Iphone 13",
    category: "IOS",
    imageUrl: "/img/ip13.png",
    price: 400,
    sold: 896,
    rating: 4.6,
    platformIcons: [AppleIcon],
    createdAt: "01/01/22",
  },
  {
    name: "SamSung galaxy zfold",
    category: "ANDROID",
    imageUrl: "/img/zfold.png",
    price: 1200,
    sold: 194,
    rating: 4.6,
    platformIcons: [SamsungIcon],
    createdAt: "04/01/22",
  },
  {
    name: "Huawei Mate X",
    category: "ANDROID",
    imageUrl: "/img/Huawei.png",
    price: 300,
    sold: 404,
    rating: 4.3,
    platformIcons: [HuaweiIcon],
    createdAt: "12/12/21",
  },
];
</script>

